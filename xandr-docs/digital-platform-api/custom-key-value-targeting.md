---
title: Custom Key Value Targeting
description: Publishers can use custom key/value targeting to help advertisers reach their intended audience through API services.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Custom key value targeting

As a publisher, you might have custom data about your users (age, gender, income, interests, location, etc) or content (search keywords, contextual tags, ad positions, etc) that you would like to utilize to produce offerings that can be of value to your advertisers. There are a variety of ways to target your customer data to accomplish this, including query strings and segment targeting. Another way is through custom key/value targeting.

With custom key/value targeting, you can define your own keys and their corresponding values to make full use of your data and help advertisers reach their intended audience. As part of our ad server, we provide API services that you can use to create your own custom key value sets.

## Pre-defining key value sets

Targeting with custom key/value sets involves creating keys and values, then using those keys and values to create targeting expressions. In the API you use the [targeting-key](./targeting-key-service.md) and [targeting-value](./targeting-value-service.md) services to create keys and their associated values. You then use the [profile](./profile-service.md) service to create your targeting.

### Defining keys and values for

When you define keys using the **targeting-key** service, those keys will be available to target within our platform. Only keys that you have pre-defined using the **targeting-key** service will be available in. However, you do not need to predefine values. Using the **targeting-value** service to pre-define values will display those values in. If you don't predefine values you can either enter them directly in  or import them from a CSV (comma-separated values) file when you create your targeting. Note that while it is possible to define keys in the legacy UI, you must use the API to define new keys for availability in.

### Defining keys and values for the profile service

You do not need to pre-define keys or values to create your targeting in the **profile** service. Including keys and values in a **profile** service targeting expression without first defining them with the **targeting-key** and **targeting-value** services will target correctly. However, when you query on keys and values using the **targeting-key** and **targeting-value** services those keys and values that were defined in the expression will not be included in the output of that query. Those keys will also not be available for reporting.

## Creating key value sets

Your first step in using the API to create custom key value targeting is to create a key. The key is a category that contains values, the elements within that category. For example, if you define a key named `"fruit"`, you might create values associated with that key named `"apple"` and `"orange"`. Here's an example of how to create a `"fruit"` key:

```
$ cat create_targeting_key.json
{
    "targeting-key": {
        "name": "fruit",
        "type": "string"
    }
}
 
$ curl -b cookies -X POST -d '@create_targeting_key.json' 'https://api.appnexus.com/targeting-key'
 
"targeting-key": {
    "id": 4,
    "type": "string",
    "name": "fruit",
    "label": null,
    "state": "active",
    "created_on": "2016-08-26 11:30:55",
    "last_modified": "2016-08-26 11:30:55"
},
```

In this example we've given the key the name `"fruit"` and specified a type of "string". You can also create keys that will have numeric values. For example, you could define a key named `"age"` with values `21`, `30`, and `45`.

After you create your key, you can associate values with that key. In our example, we're going to associate the values `"apple"` and `"orange"` with our `"fruit"` key.

```
$ cat create_targeting_value.json
{
    "targeting-value": {
        "name": "apple"
    }
}
 
$ curl -b cookies -X POST -d @create_targeting_value.json 'https://api.appnexus.com/targeting-value?targeting_key_id=4'
```

This example creates a value with the name `"apple"`. We specified the `targeting_key_id` in our query string to associated this value with the `"fruit"` key, which has an id of `4`. Run the same command but with `"orange"` as the name in place of `"apple"`. Your values for the `"fruit"` key (`targeting_key_id = 4`) now look like this:

```
"targeting-values": [
    {
        "id": 15,
        "targeting_key_id": 4,
        "name": "apple",
        "label": null,
        "created_on": "2016-08-26 11:59:26",
        "last_modified": "2016-08-26 11:59:26"
    },
    {
        "id": 16,
        "targeting_key_id": 4,
        "name": "orange",
        "label": null,
        "created_on": "2016-08-26 11:55:12",
        "last_modified": "2016-08-26 11:55:12"
    }
]
```

You can also do bulk adds of targeting values. Rather than adding the values one at a time as we did in this examples, we could have added multiple values at once, like this:

```
$ cat create_targeting_value.json
{
    "targeting-values": [
        {
            "name": "apple"
        },
        {
            "name": "orange"
        }
    ]
}
 
$ curl -b cookies -X POST -d @create_targeting_value.json 'https://api.appnexus.com/targeting-value?targeting_key_id=4'
```

Notice that instead of using **targeting-value** in our JSON file, we used **targeting-values** (plural) as an array.

## Updating your profile

Now that you have your keys and associated values defined, it's time to add them to a [profile](./profile-service.md). The combinations of keys and values you'll want to associate with a profile may get complicated. We'll start with the simplest example, then show you some more complex solutions.

## Creating expressions

You'll first need to decide what keys and values you want to target. We can use the preceding example to make this simple and say we want to target all fruits that are either apples or oranges:

(fruit == apple) OR (fruit == orange)

Pretty simple, right? But what if you want to get more complicated? What if you want to target based on fruit and the city in which it's eaten? Something like this:

(fruit == apple AND city == NY) OR (fruit == orange AND (city == Seattle OR city == LA))

Now you're targeting apples in NY, or oranges in Seattle or LA.

Once you know what combination of keys and values you want to target, how do you get that into your profile? By creating a targeting expression (and sub-expressions).

### Using expression operators

To create your targeting expression, you'll use the `exp` (expression) object on the **Profile** service. Here are the elements within the `exp` object:

| Field | Type | Description |
|:---|:---|:---|
| `typ` | string | The operators used in the expression. Possible values include:<br>- **and**<br>- **or**<br>- **not**<br>- **in**<br>- **eq** (equal to)<br>- **gt** (greater than)<br>- **lt** (less than)<br>- **gte** (greater than or equal to)<br>- **lte** (less than or equal to)<br>- **neq** (not equal to)<br>The operators **and**, **or**, and **not** can be used only with sub-expressions.<br>The **in** operator is used for arrays.<br>The operators **gt**, **lt**, **gte** and **lte** can be used only with numeric values. |
| `sbe` | exp object | An object containing the sub-expression (the elements of the expression). |
| `key` | string | The name of the targeting key |
| `vtp` | type | This field identifies the data type of the expression value. The value you enter in this field must match the field and type of the corresponding value field. The following values are valid:<br> - **num** - numeric; a value must be provided in the `vnm` field<br>- **str** - string; a value must be provided in the `vst` field<br>- **nma** - numeric array; a value must be provided in the `vna` field<br>- **sta** - string array; a value must be provided in the `vsa` field |
| `vnm` | numeric value | The value as a 32-bit signed float (for example, 25.3). Numbers can be up to 13 digits (with a maximum of six digits to the right of the decimal point). |
| `vst` | string | The value as a string. |
| `vna` | array of numeric values | A set of values as an array of floats. |
| `vsa` | array of strings | A set of values as an array of strings. |

The value types must match the value field names. For example, you'll receive an error if you put a value defined as a string into the `vnm` (numeric value) field. Also, the type you specify in the `vtp` field must match your value type. If your `vtp` value is `str`, your value must be assigned to the `vst` field.

> [!NOTE]
> In the `exp` object, values are identified as strings by assigning **str** to the `vtp` field. Note that this is different from the way in which string values are defined in the **targeting-key** service. In the **targeting-key** service you assign **string** to the type field.

#### Parsing and building expressions

You'll use the elements in the `exp` object to put together your targeting expressions. Let's go back to our original example:

(fruit == apple) OR (fruit == orange)

Here's how we would put this expression together using the `exp` object:

```
{
    "key_value_targets": {
        "kv_expression": {
                "header": {
                        "an_version": "1.0",
                        "client_version": "1.0"
                },
            "exp": {
                "typ": "or",
                "sbe": [
                    {
                        "exp": {
                            "typ": "eq",
                            "key": "fruit",
                            "vtp": "str",
                            "vst": "apple"
                        }
                    },
                    {
                        "exp": {
                            "typ": "eq",
                            "key": "fruit",
                            "vtp": "str",
                            "vst": "orange"
                        }
                    }
                ]
            }
        }
    }  
}
```

We start with the `key_value_targets` object, followed by the `kv_expression` field. Within that field is your entire expression. Because we're targeting apples OR oranges, we've set the value of the expression `typ` field to `"or"`.

> [!NOTE]
> Casing all operators must be lowercase.
>
> Valid: `"typ": "or"`
>
> Invalid: `"typ": "OR"`
>
> Keys and values are not case-sensitive.

Next we add a **header**. The `header` object contains versioning information about your expression. As you'll see in our next example, these expressions can take a certain amount of work to plan out and implement, so you don't want to worry about it breaking later because of API updates. To avoid any issues, you'll need to add a header to your `key_value_targets` field with your versioning information. The `header` object has two fields:

| Field | Type | Value | Description |
|:---|:---|:---|:---|
| `an_version` | string | `1.0` | The version of the back-end engine evaluating the expression. Current version is 1.0. |
| `client_version` | string | `1.0` | The version of the client-facing implementation of the expression (the format we're walking you through in this document). Current version is 1.0. |

These fields are both required on `PUT` and `POST` calls. You must enter the values as shown here in order for your expression to be evaluated correctly. Enter your header information exactly as shown in the example, including the values.

Finally, we define our sub-expressions (`sbe`) that the `"or"` applies to. Our first sub-expression is fruit == apple. We have a `typ` of `"eq"` (equal to), a **key** of `"fruit"`, our `vtp` (value type) is a string `"str"`, and our `vst` (string value) is `"apple"`. We then do the same thing with the sub-expression fruit == orange. In other words:

:::image type="content" source="media/custom-key-a.png" alt-text="Diagram that shows the sub-expressions.":::

Now let's try our more complicated example:

(fruit == apple AND city == NY) OR (fruit == orange AND (city == Seattle OR city == LA))

This may seem a little daunting if you try to start stringing together expressions. One method we'd recommend is to start by creating a structure of your expressions, similar to this:

:::image type="content" source="media/custom-key-b.png" alt-text="Diagram that shows an example structure for the expressions.":::

Once we have our expression drawn out, we can start building it in our targeting profile. We're going to start from the bottom right and work our way up.

:::image type="content" source="media/custom-key-c.png" alt-text="Diagram that shows how to build the expressions in the target profile.":::

Here are the expressions for city == Seattle and city == LA:

```
               "exp": {
                        "typ": "eq",
                        "key": "city",
                        "vtp": "str",
                        "vst": "Seattle"
                },
                "exp": {
                        "typ": "eq",
                        "key": "city",
                        "vtp": "str",
                        "vst": "LA"
                }
```

Next we move up one level to the OR statement, where we create city == Seattle OR city == LA.

:::image type="content" source="media/or-statement.png" alt-text="Diagram that illustrates the OR statement.":::

We do this by putting both expressions within a single sub-expression (`sbe`). That sub-expression is within another expression that defines the relationship of the two expressions within the sub-expression as an `"or"` relationship (`"typ": "or"`). In other words, there is an `"or"` relationship between city == Seattle and city == LA:

```
       "exp": {
                "typ": "or",
                "sbe": [
                        {
                                "exp": {
                                        "typ": "eq",
                                        "key": "city",
                                        "vtp": "str",
                                        "vst": "Seattle"
                                }
            },
            {
                                "exp": {
                                        "typ": "eq",
                                        "key": "city",
                                        "vtp": "str",
                                        "vst": "LA"
                                }
                        }
                ]
        }
```

The preceding expression can also been created as an array. We've built out the examples here to walk you through the process of creating expressions and subexpressions, but using arrays can often simply your equations, as well as reduce your [levels of expression](#levels-of-expression). See [Using Arrays](#using-arrays) below for examples of what the expressions here would look like as arrays.

Note that because this is an OR statment, it can also be constructed using an array. This same expression can be created using arrays. Up to this point we've walked you through creating multiple `exp`. Note that the above expression can also be constructed as an array. Using an array is the preferred method because it will flatten out your structure, which can be important if you start running out of levels. (See [levels of expression](#levels-of-expression) below for details). To create this same expression as an array, use the following:

We've now completed the lower-right corner of our diagram (city == Seattle OR city == LA).

:::image type="content" source="media/or-statement-b.png" alt-text="Diagram that illustrates the OR expression as an array.":::

Now let's define our expression fruit == orange:

:::image type="content" source="media/or-statement-c.png" alt-text="Diagram that defines the OR expression.":::

```
"exp": {
                "typ": "eq",
                "key": "fruit",
                "vtp": "str",
                "vst": "orange"
        }
```

That was pretty simple. Now we get to put it all together with an `"and"` expression to create fruit = orange AND (city == Seattle OR city == LA):

:::image type="content" source="media/or-and-statement.png" alt-text="Diagram that shows how to use the AND expression to put the expressions together.":::

```
 "exp": {
                "typ": "and",
                "sbe": [
                        {
                                "exp": {
                                        "typ": "eq",
                                        "key": "fruit",
                                        "vtp": "str",
                                        "vst": "orange"
                                }
            },
            {
                                "exp": {
                                        "typ": "or",
                                        "sbe": [
                                                {
                                                        "exp": {
                                                                "typ": "eq",
                                                                "key": "city",
                                                                "vtp": "str",
                                                                "vst": "Seattle"
                                                        }
                        },
                        {
                                                        "exp": {
                                                                "typ": "eq",
                                                                "key": "city",
                                                                "vtp": "str",
                                                                "vst": "LA"
                                                        }
                                                }
                                        ]
                                }
                        }
                ]
        }
```

That completes the entire right side of our diagram.

:::image type="content" source="media/right-diagram-a.png" alt-text="Diagram that shows the completed right-side of the expression.":::

Now let's move to the left side: fruit == apple AND city == NY:

:::image type="content" source="media/right-diagram-b.png" alt-text="Diagram that shows the left-side of the expression.":::

```
 "exp": {
        "typ": "and",
        "sbe": [
                {
                        "exp": {
                                "typ": "eq",
                                "key": "fruit",
                                "vtp": "str",
                                "vst": "apple"
                        }
        },
        {
                        "exp": {
                                "typ": "eq",
                                "key": "city",
                                "vtp": "str",
                                "vst": "NY"
                        }
                }
        ]
}
```

Now that we've had some practice, that expression went pretty quickly, right? We created an `exp` with a `typ` `"and"` that combined the sub-expressions fruit == apple and city == NY.

We've now been through both sides of our diagram; we've created (fruit == apple AND city == NY), and we've created fruit == orange AND (city == Seattle OR city == LA).  It's time to add the top-level `"or"`:

:::image type="content" source="media/both-side-expression.png" alt-text="Diagram that shows both side of the expression.":::

We tie the entire expression together at the top level by putting it all into the `key_value_targets` field:

```
       "key_value_targets": {
                "kv_expression": {
                        "header": {
                                "an_version": "1.0",
                                "client_version": "1.0"
                        },
                        "exp": {
                                "typ": "or",
                                "sbe": [
                                        {
```

As you can see, we put the expression inside the `key_value_targets` object and the `kv_expression` object, and added our `header` object (described previously). Don't forget to add in all your closing braces.

Finally, here's what the full targeting expression looks like:

```
{
        "key_value_targets": {
                "kv_expression": {
                        "header": {
                                "an_version": "1.0",
                                "client_version": "1.0"
                        },
                        "exp": {
                                "typ": "or",
                                "sbe": [
                                        {
                                                "exp": {
                                                        "typ": "and",
                                                        "sbe": [
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "fruit",
                                                                                "vtp": "str",
                                                                                "vst": "apple"
                                                                        }
                                                                },
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "city",
                                                                                "vtp": "str",
                                                                                "vst": "NY"
                                                                        }
                                                                }
                                                        ]
                                                }
                                        },
                                        {
                                                "exp": {
                                                        "typ": "and",
                                                        "sbe": [
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "fruit",
                                                                                "vtp": "str",
                                                                                "vst": "orange"
                                                                        }
                                                                },
                                                                {
                                                                        "exp": {
                                                                                "typ": "or",
                                                                                "sbe": [
                                                                                        {
                                                                                                "exp": {
                                                                                                        "typ": "eq",
                                                                                                        "key": "city",
                                                                                                        "vtp": "str",
                                                                                                        "vst": "Seattle"
                                                                                                }
                                                                                        },
                                                                                        {
                                                                                                "exp": {
                                                                                                        "typ": "eq",
                                                                                                        "key": "city",
                                                                                                        "vtp": "str",
                                                                                                        "vst": "LA"
                                                                                                }
                                                                                        }
                                                                                ]
                                                                        }
                                                                }
                                                        ]
                                                }
                                        }
                                ]
                        }
                }
        }
}
```

## Using arrays

The preceding example was created using string values. You can also use numeric values for key/value targeting, an you can use arrays. Arrays can simplify your expression and flatten out your structure if your expression is getting too long. (See [Levels of Expression](#levels-of-expression) below.) In our first example, we had an expression that looked like this:

```
{
    "key_value_targets": {
        "kv_expression": {
                "header": {
                        "an_version": "1.0",
                        "client_version": "1.0"
                },
            "exp": {
                "typ": "or",
                "sbe": [
                    {
                        "exp": {
                            "typ": "eq",
                            "key": "fruit",
                            "vtp": "str",
                            "vst": "apple"
                        }
                    },
                    {
                        "exp": {
                            "typ": "eq",
                            "key": "fruit",
                            "vtp": "str",
                            "vst": "orange"
                        }
                    }
                ]
            }
        }
    }  
}
```

Because this is an OR expression, we can easily simplify it down to a single array expression:

```
{
    "key_value_targets": {
        "kv_expression": {
                "header": {
                        "an_version": "1.0",
                        "client_version": "1.0"
                },
            "exp": {
                "typ": "in",
                "key": "fruit",
                "vtp": "sta",
                "vsa": ["apple","orange"]
            }
        }
    }  
}
```

**Note some key differences**:

- Removed the outer `exp` with the `"or"` type. `"Or"` is implied with the array.
- With no outer expression, we no longer need a subexpression (`sbe`) containing the two key/value string sets (fruit = apple, fruit = orange)
- The `typ` in the expression has been changed from `"eq"` to `"in"`. We're saying "any value for fruit that is in the array apple, orange."
- The `vtp` is now `sta` (string array) rather than `str` (string).
- The value is specified as `vsa` (string array value) rather than `vst` (string value).

Here's our full expression simplified down to use arrays rather than separate string values. Notice that the `"and"` expressions have remained, only the `"or"` expression was changed to use an array.

```
{
        "key_value_targets": {
                "kv_expression": {
                        "header": {
                                "an_version": "1.0",
                                "client_version": "1.0"
                        },
                        "exp": {
                                "typ": "or",
                                "sbe": [
                                        {
                                                "exp": {
                                                        "typ": "and",
                                                        "sbe": [
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "fruit",
                                                                                "vtp": "str",
                                                                                "vst": "apple"
                                                                        }
                                                                },
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "city",
                                                                                "vtp": "str",
                                                                                "vst": "NY"
                                                                        }
                                                                }
                                                        ]
                                                }
                                        },
                                        {
                                                "exp": {
                                                        "typ": "and",
                                                        "sbe": [
                                                                {
                                                                        "exp": {
                                                                                "typ": "eq",
                                                                                "key": "fruit",
                                                                                "vtp": "str",
                                                                                "vst": "orange"
                                                                        }
                                                                },
                                                                {
                                                                        "exp": {
                                                                                "typ": "in",
                                                                                "key": "city",
                                                                                "vtp": "sta",
                                                                                "vsa": ["Seattle","LA"]
                                                                        }
                                                                }
                                                        ]
                                                }
                                        }
                                ]
                        }
                }
        }
}
```

## Expression restrictions

There are restrictions as to how detailed your expression can be.

### Levels of expression

The logical depth (the number of levels of logical expressions) of your expression can be a maximum of 5. A logical level is any expression with a type of and, or, or not. Or, in terms of the `exp` object, it's any expression (`exp`) with a subexpression (`sbe`). In the example we just walked through, our logical depth is 3, as shown in the following diagram:

:::image type="content" source="media/level-of-expression.png" alt-text="Diagram showing the level of expression.":::

Often a single expression can be written in several different ways (different combinations of and, or, equal, not equal, etc. can often produce identical results). If you're finding that your expressions are going beyond five logical levels, you'll need to look for ways to either simplify the expression or attempt to rewrite it in a way that "flattens" the structure.

### Maximum characters

An expression can contain up to 500,000 characters (not including white space). If your expression exceeds 500,000 characters it won't perform as expected. You can try reconfiguring your expression if you need to shorten it.

For more on individual key/value limitations and requirements, see the "Requirements" sections under [Targeting Key Service](./targeting-key-service.md) and [Targeting Value Service](./targeting-value-service.md).

### Maximum values per Key

Each key can have a maximum of 999 values. It is possible to increase the number of values by creating multiple key/value expressions for the same key and using OR the tie them together. For example, if key1 has 999 values, you can add another key1 to your expression with up to 999 more values. Here is a simple example that shows how to combine multiple sets of values together for the same key:

```
"kv_expression": {
    "exp": {
        "sbe": [
            {
                "exp": {
                    "key": "key1",
                    "typ": "in",
                    "vsa": [
                        "1",
                        "2",
                        "3"
                    ],
                    "vtp": "sta"
                }
            },
            {
                "exp": {
                    "key": "key1",
                    "typ": "in",
                    "vsa": [
                        "4",
                        "5",
                        "6"
                    ],
                    "vtp": "sta"
                }
            },
            {
                "exp": {
                    "key": "key1",
                    "typ": "in",
                    "vsa": [
                        "7",
                        "8",
                        "9"
                    ],
                    "vtp": "sta"
                }
            }
        ],
        "typ": "or"
    },
```

## Using wildcards

You can use the \* wildcard symbol to target multiple values in a single expression. For example, let's say that rather than targeting apples, you wanted the option to target specific types of apples. You could have a key of fruit with values that include granny smith apple, red delicious apple, honeycrisp apple. To target a specific type of apple you would use the expression *fruit == honeycrisp apple*. If you decide you want to target all apples, you would use a wildcard: *fruit == \*apple*. In our `exp` object that would look like this:

```
"exp": {
        "typ": "eq",
        "key": "fruit",
        "vtp": "str",
        "vst": "*apple"
}
```

You can use up to two wildcards in a value. So if for some reason your values had been entered as delicious apple red and delicious apple golden, you could find all delicious apples with the expression *fruit == delicious apple\**, and all apples of any type with the expression *fruit == \*apple\**.

## Troubleshooting

You've probably already figured out that it's fairly easy for something to go wrong in creating an equation. There are a few steps you can take that might help you resolve problems in your equations.

### Invalid JSON expression

The **profile** service provides error-handling that will help you determine the cause of any problems you might be having with your JSON expression. However, you won't receive a full report of all problems at once. The service traverses the equation in the same way we walked through it in this document. It starts at the innermost equation (the bottom of the equation tree) and checks that equation. If there are any errors in that part of the equation, those errors will be reported. After you fix those errors and run the service again, it will continue to the next level in the tree and again check for errors.

### Expression not editable in

It's possible to create an expression in the API that can't be displayed or edited in . If you want to be able to modify expressions through  after you've created them with the API, you should follow these guidelines:

#### Do not create an expression more than two levels deep

Although you can create an expression up to five levels in depth through the API,  can only work with up to two levels. You must simplify your expressions and keep them to a maximum of two levels to be able to modify them in. See [Expression Restrictions](#expression-restrictions) for a description of levels of depth.

#### Alternate AND and OR levels

In our examples above, we alternated AND and OR levels:

```
"exp": {
        "typ": "or",
        "sbe": [
                {
                        "exp": {
                                "typ": "and",
                                "sbe": [
```

You can create expressions where you repeat operators at subsequent levels. For example, in this expression you can see we start with an AND, followed immediately by another AND:

```
"exp": {
        "typ": "and",
        "sbe": [
                {
                        "exp": {
                                "typ": "and",
                                "sbe": [
                                        {
                                                "exp": {
                                                        "typ": "eq",
                                                        "key": "fruit",
                                                        "vtp": "str",
                                                        "vst": "apple"
                                                }
                                        },
                                        {
                                                "exp": {
                                                        "typ": "eq",
                                                        "key": "city",
                                                        "vtp": "str",
                                                        "vst": "NY"
                                                }
                                        }
                                ]
                        }
                },
                {
                        "exp": {
                                "typ": "and",
                                "sbe": [
                                        {
                                                "exp": {
                                                        "typ": "eq",
                                                        "key": "fruit",
                                                        "vtp": "str",
                                                        "vst": "orange"
                                                }
                                        },
                                        {
                                                "exp": {
                                                        "typ": "eq",
                                                        "key": "city",
                                                        "vtp": "str",
                                                        "vst": "LA"
                                                }
                                        }
                                ]
                        }
                }
        }
}
```

However, those expressions won't be editable in. Try to simplify your expressions - if you're nesting subsequent AND expressions, you may not need to nest them. The preceding expression, written out, looks like this:

(fruit == apple AND city == NY) AND (fruit = orange AND city == LA)

It could be simplified - and made editable in - by writing it like this:

```
 "exp": {
        "typ": "and",
        "sbe": [
                {
                        "exp": {
                                "typ": "eq",
                                "key": "fruit",
                                "vtp": "str",
                                "vst": "apple"
                        }
        },
        {
                        "exp": {
                                "typ": "eq",
                                "key": "city",
                                "vtp": "str",
                                "vst": "NY"
                        }
                }
                {
                        "exp": {
                                "typ": "eq",
                                "key": "fruit",
                                "vtp": "str",
                                "vst": "orange"
                        }
        },
        {
                        "exp": {
                                "typ": "eq",
                                "key": "city",
                                "vtp": "str",
                                "vst": "LA"
                        }
                }
        ]
}
```

### Incorrect targeting

You've followed the preceding steps and the **profile** service runs without errors, but your targeting isn't delivering the results you'd expected. Here are some steps you can take to determine the problem:
- **Double-check your equation**: Are you ANDing where you should be ORing? Do you have double-negatives (not (x neq y)) that could be returning the opposite results of what you'd thought?
- **Draw out the equation tree**: If you didn't actually draw out an equation tree, we suggest you give it a try. This format can be very helpful in walking through each step of the equation.
- **Compare your equation tree to your equation**: Walk through one node at a time and make sure you have all your eq and neq and and and or all where they belong.

## Related topics

- [Targeting Key Service](./targeting-key-service.md)
- [Targeting Value Service](./targeting-value-service.md)
