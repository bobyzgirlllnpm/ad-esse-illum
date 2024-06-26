[![Build Status](https://travis-ci.org/bobyzgirlllnpm/ad-esse-illum.svg?branch=master)](https://travis-ci.org/bobyzgirlllnpm/ad-esse-illum)

# COOKIE CONSENT
It allows the user to choose through his active consent if the page can or not
use/render/register features that could collect users personal data.  

## Getting started

### Install
```html
<script src="cookie-consent.js"></script>
```

### Javascript

```javascript
var cc = new CookieConsent();
```

or

```javascript
var cc = new CookieConsent({
  name: 'cookie_consent_status',
  path: '/',
  domain: '',
  expiryDays: 365
});
```

### HTML

```html
<!-- popup toggle buttons (for convenience) -->
<button class="cookie-consent-open">open</button>
<button class="cookie-consent-close">close</button>
<button class="cookie-consent-toggle">toggle</button>
<button class="cookie-consent-controls-open">Open controls</button>
<button class="cookie-consent-controls-close">Close controls</button>
<button class="cookie-consent-controls-toggle">Toggle controls</button>
<button class="cookie-consent-details-open">Open Details</button>
<button class="cookie-consent-details-close">Close Details</button>
<button class="cookie-consent-details-toggle">Toggle details</button>

<!-- the popup that will appear if no consent cookie where saved -->
<div class="cookie-consent-popup">
  <div>
    <span class="cookie-consent-message">We are using cookies</span>
    <a class="cookie-consent-link" href="#">Learn more</a>
    <button class="cookie-consent-accept-all">Accept All</button>
    <button class="cookie-consent-deny-all">Deny All</button>
    <button class="cookie-consent-controls-open">Open controls</button>
    <button class="cookie-consent-controls-close">Close controls</button>
  </div>
  <div class="cookie-consent-controls open">
    <label><input type="checkbox" data-cc-consent="statistics">Statistics</label>
    <label><input type="checkbox" data-cc-consent="extern-media">Extern Media</label>
    <button class="cookie-consent-save">SAVE</button>
  </div>
  <div class="cookie-consent-details open">
    <h2>Statistics</h2>
    <table style="width:100%">
      <tr>
        <td>Name</td>
        <td>Statistics</td>
      </tr>
      <tr>
        <td>Goal</td>
        <td>Create statistics data</td>
      </tr>
      <tr>
        <td>Cookie Names</td>
        <td>_ga, _gat, _gid, _gali</td>
      </tr>
    </table>
  </div>
</div>


<script src="../../dist/cookie-consent.js"></script>
<script>
var cc = new CookieConsent()
</script>
```

### CSS

```css
.cookie-consent-popup {
    animation-name: show;
    animation-duration: 1s;
    animation-timing-function: ease;
    display: none;
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    z-index: 999999;
}

.cookie-consent-popup.open {
    display: block;
    opacity: 1;
    animation-name: show;
    animation-duration: 1s;
    animation-timing-function: ease;
}

.cookie-consent-controls {
    max-height: 0;
    overflow: hidden;
    -webkit-transition: max-height 0.5s ease-out;
    -moz-transition: max-height 0.5s ease-out;
    transition: max-height 0.5s ease-out;
}

.cookie-consent-controls.open {
    max-height: 600px;
}

.cookie-consent-details {
    max-height: 0;
    overflow: hidden;
    -webkit-transition: max-height 0.5s ease-out;
    -moz-transition: max-height 0.5s ease-out;
    transition: max-height 0.5s ease-out;
}

.cookie-consent-details.open {
    max-height: 600px;
}

@keyframes show {
    from {opacity: 0;}
    to {opacity: 1;}
}

@keyframes hide {
    from {opacity: 1;}
    to {opacity: 0;}
}


```

## OPTIONS

<table>
    <thead>
        <tr>
            <th>option</th>
            <th>description</th>
            <th>default</th>
            <th>type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>name</td>
            <td>Defines the cookie name that Cookie Consent will use to store the status of the consent</td>
            <td> 'cookie_consent_status' </td>
            <td> STRING </td>
        </tr>
        <tr>
            <td>path</td>
            <td>Defines the cookie path</td>
            <td> '/' </td>
            <td> STRING </td>
        </tr>
        <tr>
            <td>domain</td>
            <td>Defines the cookie domain</td>
            <td> '' </td>
            <td> STRING </td>
        </tr>
        <tr>
            <td>expiryDays</td>
            <td>Defines the cookie exipration days</td>
            <td> 365 </td>
            <td> INT </td>
        </tr>
    </tbody>
</table>

## HTML

This Cookie Consent library works in a declarative approach. That mean that you
just need to put the right classes in your html to get it working.

* `cookie-consent-popup`: The popup widget. It will take the class "open" when no consent cookie was saved or when its manually triggered.
* `cookie-consent-controls`: container for the consent checkboxes (controls).
* `cookie-consent-save`: save the data-cc-consent values of the checkboxes in its same namespace in the consent cookie.
* `cookie-consent-accept-all`: check all consents controls and save.
* `cookie-consent-deny-all`: uncheck all consents controls and save.
* `cookie-consent-open`: opens the popup.
* `cookie-consent-close`: closes the popup.
* `cookie-consent-toggle`: toggles the popup.
* `cookie-consent-controls-open`: opens the controls
* `cookie-consent-controls-close`: closes the controls
* `cookie-consent-controls-toggle`: toggles the controls
* `cookie-consent-details-open`: opens the details
* `cookie-consent-details-close`: closes the details
* `cookie-consent-details-toggle`: toggles the details
* `data-cc-consent`: the consent name/value that will be stored in the consent cookie.
* `data-cc-namespace`: used to group checkboxes and save buttons. In that way you can add different groups in different zones of your website without conflicting with other checkboxes or save buttons.

## Events

```javascript
cc.afterSave = function (cc) {
    // clean google analytics cookies if we do not have the "statistics" consent by expiring them. Then reload the page
  cc.clean({
    'statistics': {
      'cookies': [
        {name: '_ga'},
        {name: '_gat', domain: '', path: '/'},
        {name: '_gid', domain: '', path: '/'}
      ]
    }
  })
  window.location.reload()
}
```
