---
Title : Native Assembly Renderer Best Practices
Description : The Renderer tab stores the HTML, CSS,
ms.date: 10/28/2023
and Javascript code associated with the native assembly. Any changes
---


# Native Assembly Renderer Best Practices



The Renderer tab stores the HTML, CSS,
and Javascript code associated with the native assembly. Any changes
made on the Renderer tab will
automatically be reflected in the
Preview window.





Here's a list of tips and important notes related to the
Renderer tab that you should keep
in mind:

- If you removed any of the existing standard and custom creative asset
  specifications on the Setup tab, the
  HTML code on the Renderer tab won't
  automatically reflect this change, so manually remove the
  corresponding HTML and/or placeholders from the
  HTML text box on the
  Renderer tab.
- Ensure that the `[%impressionTrackers%]` object placeholder appears in
  the HTML field or
  Javascript field on the
  Renderer tab. If it doesn't, you'll
  have to manually add it so that impression trackers can be tracked. If
  your renderer or website uses another impression tracking method, you
  don’t have to add the `[%impressionTrackers%]` object placeholder to
  the HTML field or
  Javascript field. However, when
  saving your native assembly, a warning dialog will appear where you
  can select the I will manage my impression
  trackers from my own website checkbox, which gives you the
  ability to save the native assembly without adding the
  `[%impressionTrackers%]` object placeholder.
- Adding `<script>` tags directly in the
  HTML text box won't work. You must
  use the designated Javascript text
  box to write js code. The Javascript
  text box doesn't require the user to use HTML `<script>` tags.
- Following <a
  href="https://www.iab.com/wp-content/uploads/2017/08/IABNewAdPortfolio_FINAL_2017.pdf#page=20"
  class="xref" target="_blank">IAB's standard for video creatives</a>,
  by default, native videos will play when the user clicks the play
  button. If you want the video to play automatically with the audio
  muted, remove the `//` from these commented lines under
  `function vidCallback()` in the
  Javascript text box on the
  Renderer tab:
  

  ``` pre
  //initialPlayback: 'auto',
  //initialAudio: 'off'
  ```

  



Related Topics

- <a href="configuring-a-native-assembly.md" class="xref"
  title="Monetize Ad Server and third-party ad server publishers can configure native assemblies by selecting various creative asset specifications directly from the UI or creating custom HTML, CSS, and Javascript. You must associate all native assemblies to a placement in order for them to go live.">Configuring
  a Native Assembly</a>






