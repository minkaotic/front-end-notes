# Accessibility
Sources: [Accessibility for Web Developers](https://teamtreehouse.com/library/accessibility-for-web-developers) | [Web Accessibility Compliance](https://teamtreehouse.com/library/web-accessibility-compliance)

### Contents

- [WCAG Overview](#-wcag-overview)
- [Tools for Accessibility Auditing](#%EF%B8%8F-tools-for-accessibility-auditing)

-------------

## 🌐 WCAG Overview
The [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/) state that in order to be accessible, interfaces must follow **4 principles** (*POUR* - see below). WCAG 2 introduced **13 guidelines** to meet these principles, further broken down into **78 success criteria**. Two great resources for learning these are:
- [Exploring The New Success Criteria](https://www.levelaccess.com/wcag-2-1-exploring-new-success-criteria/)
- [13 Days of Accessibility](http://a11ycalendar.kaseybon.com/)

The success criteria are at **3 levels**: A, AA and AAA. On the modern web, achieving level A compliance should be easily within reach, and level AA should be the minimum accessibility standard for most projects.

- **Perceivable** - information and user interface components must be presentable to users in ways they can perceive. This principle is all about providing alternative methods of understanding your web content. Its guidelines cover:
  - text alternatives (e.g. `alt` attribute)
  - time-based media (e.g. providing captions and transcripts)
  - adaptable (e.g. use semantic HTML in a logical order; interfaces should be navigable in portrait as well as landscape orientation)
  - distinguishable (e.g. colour contrast; combine multiple visual cues incl. messaging/iconography rather than relying on colour alone to convey information; avoid auto-starting audio or video; website can be resized to 200% without loss of content/functionality)
- **Operable** - users must be able to operate your interface without barriers. This principle covers:
  - keyboard-access (navigable via tab key; no keyboard traps; have obvious focus indicators and logical focus order)
  - enough time (users should be able to adjust or remove time limits on bookings etc. if they need extra time)
  - seizures + physical reactions (allow users to disable distracting content; avoid animations that flash more than 3 times/second)
  - navigable (use proper HTML structure of [headings in a logical hierarchy](https://usability.yale.edu/web-accessibility/articles/headings) and semantic containers - this also helps skip content that is repeated on multiple pages, such as navigation; provide a descriptive page `<title>` tag; purpose of a link should be clear from the link text, i.e. avoid 'click here' being the link)
  - input modalities (provide alternatives to complex interactions, e.g. complex touch screen gestures; use generous target sizes)
- **Understandable**
  - readable
  - predictable
  - input assistance 
- **Robust**
  - compantible


#### For visual impairments
- Use good colour contrast
- Use accessible fonts such as Arial, Calibri, Century gothic, Helvetica, Tahoma and Verdana
- Make sure images have descriptive `alt` text where appropriate

#### For audio impairments
- Provide subtitles and captions for videos
- Provide transcripts
- Include context explaining the video

#### For motor impairments
- Provide global navigation menu
- Ensure users can navigate through keyboard
- Avoid dynamic and gesture-based content

#### For cognitive impairments
- Provide clear steps and direction
- Allow the user to focus on one thing at a time
- Provide sufficient context


## 🛠️ Tools for Accessibility Auditing
- Turn your CSS off so you can see a simpler version of the site
- Zoom to 200% and ensure all parts of your site can still be accessed
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [WebAIM colour contrast checker](https://webaim.org/resources/contrastchecker/)
- [Axe](https://www.deque.com/axe/) and [WAVE](https://wave.webaim.org/extension/) - browser extensions to evaluate web accessibility
- NoCoffee
- Voiceover (Mac only)
