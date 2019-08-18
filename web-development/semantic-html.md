# Semantic HTML

Expresses the meaning behind the content that is being displayed.

Reserve divs for grouping elements purely for styling purposes.

Auditing a site
- Is the HTML descriptive of its content?
- How is our content structured?
    - HTML is building an outline which can be used by search engines. 
- Are any elements used presentationally?
    - Use CSS instead.
    - e.g. bold, 

## Sectioning and grouping elements

Sectioning elements
- header
- footer
- main
- section
- article
- aside
- address
- figure
- nav 

## Implicit sections as outine for your content

Level headings define sections implicitely. Use headings as delimiters of your content's outline.

e.g. subheadings shouldn't be marked with a heading tag. Use the `<p>` tag

## Text-level semantic elements

Text level elements
- a
- em
    - for emphasising the text enclosed
- strong
- small
    - for side comments like disclaimers, caveats, legal restrictions, copyrights, or attribution.
- cite
    - for citations
- dfn
- abbr
    - for abbreviations or acronyms
- time
    - for time or precise date
- span
- b
- i

## Sematic forms

Semantic form elements
- form
    - label
        - input
            - specify a descriptive input type
            - e.g. email, date, etc...
    - fieldset
        - legend