# Handlebars by Pug

[Pug mixins](https://pugjs.org/language/mixins.html) for the outputting of the [Handlebars](https://handlebarsjs.com/guide/) code instead of plain HTML.


## Installation

```bash
npm i handlebars-by-pug -D -E
```


## Functionality

### Will work with plain Handlebars

#### `HandlebarsCondition`

```pug
dl

  dt.MemberProfile-Profile-KeyCell Full Name
  dd.MemberProfile-Profile-ValueCell {{ fullName }}

  +HandlebarsCondition("phoneNumber")
    dt.MemberProfile-Profile-KeyCell Phone number
    dd.MemberProfile-Profile-ValueCell {{ phoneNumber }}
```

Output (manually formatted):

```handlebars
<dl>
    
  <dt class="MemberProfile-Profile-KeyCell">Full Name</dt>
  <dd class="MemberProfile-Profile-ValueCell">{{ fullName }}</dd>
    
  {{#if phoneNumber}}
    <dt class="MemberProfile-Profile-KeyCell">Phone number</dt>
    <dd class="MemberProfile-Profile-ValueCell">{{ phoneNumber }}</dd>
  {{/if}}
    
</dl>
```


#### `HandlebarsIteration`

```pug
+HandlebarsCondition("items")
  
  ul
  
    +HandlebarsIteration("items")
    
      li {{ this }}
```

Output (manually formatted):

```handlebars
{{#if items}}
  <ul>
    {{#each items}}
      <li>{{ this }}</li>
    {{/each}}
  </ul>
{{/if}}
```

#### HandlebarsHelper

```pug
+HandlebarsHelper("unless", "license")
  p WARNING: This entry does not have a license!
```

Output (manually formatted):

```handlebars
{{#unless license}}
    <p>WARNING: This entry does not have a license!</p>
{{/unless}}
```


### Depends on `@yamato-daiwa/handlebars-extensions`

```bash
npm i @yamato-daiwa/handlebars-extensions -E
```

### `AreStringsEqual--HandlebarsHelper` 

```pug
dl

  dt Full Name
  dd {{ fullName }}

  +HandlebarsHelper("isNonEmptyObject", "socialNetworkProfilesURIs")
  
    dt Social networks
    dd
  
      ul
        +HandlebarsIteration("socialNetworkProfilesURIs")
          li
  
            +AreStringsEqual--HandlebarsHelper("@key", "facebook")
              a(href=`{{ this }}`)
                svg
                  // The SVG code of teh Facebook icon ... 
  
            +AreStringsEqual--HandlebarsHelper("@key", "instagram")
              a(href=`{{ this }}`)
                svg
                  // The SVG code of teh Instagram icon ...
  
            +AreStringsEqual--HandlebarsHelper("@key", "twitter")
              a(href=`{{ this }}`)
                svg
                  // The SVG code of teh Twitter icon ...
```

Output (manually formatted):

```handlebars
<dl>
    
  <dt>Full Name</dt>
  <dd>{{ fullName }}</dd>
    
  {{#isNonEmptyObject socialNetworkProfilesURIs}}
    <dt>Social networks</dt>
    <dd>
      <ul>
           
        {{#each socialNetworkProfilesURIs}}
           
          <li>
              
            {{#areStringsEqual @key "facebook"}}
              <a href="{{ this }}">
                <svg>
                  <!-- The SVG code of teh Facebook icon ... -->
                </svg>
              </a>
            {{/areStringsEqual}}
                 
            {{#areStringsEqual @key "instagram"}}
             <a href="{{ this }}">
              <svg>
                <!-- The SVG code of teh Instagram icon ...-->
              </svg>
             </a>
            {{/areStringsEqual}}
              
            {{#areStringsEqual @key "twitter"}}
              <a href="{{ this }}">
                <svg>
                  <!-- The SVG code of teh Twitter icon ...-->
                </svg>
              </a>
            {{/areStringsEqual}}
              
          </li>
        
        {{/each}}
          
      </ul>
        
    </dd>
  {{/isNonEmptyObject}}
    
</dl>
```
