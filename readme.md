# Credit Card Input form
A Component to add credit card input to your react native application. For Android & iOS.

*Forked from the original project in order to improve usability and forked again to fixed a bug of image when the app try to load a image from card* since users often recognize the have input a wrong card number only after typing the name, to have an horizontal form extending outside the view seems to be appealing but it's useless to come back. The only way to go on the first field (card number) in the original project was to click one by one all previous fields in order to restore the scroll axis (this could have been fixed with a scrollable=true property). Furthermore it's pretty unusual to have x-axis forms on a mobile ux and users do prefer fields that are always visible. It has also been implemented a new style form following the iOS10 design.

Code:

```js
// fullpage with credit card flipcard
<CreditCardInput onChange={this._onChange} />
// single-line with horizontal scrolling
<LiteCreditCardInput onChange={this._onChange} /> 
```

<p align="left">
<img src="https://github.com/lexor90/react-native-credit-card-input/blob/master/example.gif?raw=true" width=200/>
</p>

# Features
* [iOS 10 form design](https://github.com/lexor90/react-native-credit-card-input/blob/master/form.png?raw=true)
* Customizable credit card that flips as you type to show credit card fields (inspired by: [card](https://jessepollak.github.io/card/), [react-native-credit-card](https://github.com/sonnylazuardi/react-native-credit-card))
* Scalable credit card
* Lite version for smaller screens
* Credit-card input validations & formatting as you type
* Integrated with [card-validator](https://github.com/braintree/card-validator) by braintree to display credit card type
* Auto-focus next field as you complete correctly one
* iOS native form design (customizable if you want to)

# TODO
* Add Android form design

# Usage

```bash
npm i --save react-native-credit-card-input-fullpage
```

then add these lines in your react-native codebase

```js
import { CreditCardInput, LiteCreditCardInput } from "react-native-credit-card-input";

<CreditCardInput onChange={this._onChange} />
// or
<LiteCreditCardInput onChange={this._onChange} />

// Note: You'll need to enable LayoutAnimation on android to see LiteCreditCardInput's animations
// UIManager.setLayoutAnimationEnabledExperimental(true);

```

And then on your onChange handler:

```js
_onChange => form => console.log(form);

// will print:
{
  valid: true, // will be true once all fields are "valid" (time to enable the submit button)
  values: { // will be in the sanitized and formatted form
  	number: "4242 4242",
  	expiry: "06/19",
  	cvc: "300",
  	type: "visa", // will be one of [null, "visa", "master-card", "american-express", "diners-club", "discover", "jcb", "unionpay", "maestro"]
  	name: "Sam",
  	postalCode: "34567",
  },
  status: {  // will be one of ["incomplete", "invalid", and "valid"]
	number: "incomplete",
	expiry: "incomplete",
	cvc: "incomplete",
	name: "incomplete", 
	postalCode: "incomplete",
  },
};

// Notes: 
// cvc, name, & postalCode will only be available when the respective props is enabled (e.g. requiresName, requiresCVC)
```

# Props

## LiteCreditCardInput
| Property | Type | Description |
| --- | --- | --- | --- |
|autoFocus | PropTypes.bool | Automatically focus Card Number field on render|
|onChange | PropTypes.func | Receives a `formData` object every time the form changes |
|onFocus | PropTypes.func | Receives the name of currently focused field |
|placeholders | PropTypes.object | Defaults to <br/>`{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" }` |
|inputStyle | Text.propTypes.style | Style for credit-card form's textInput |
|validColor | PropTypes.string | Color that will be applied for valid text input. Defaults to: "{inputStyle.color}" |
|invalidColor | PropTypes.string | Color that will be applied for invalid text input. Defaults to: "red" |
|placeholderColor | PropTypes.string | Color that will be applied for text input placeholder. Defaults to: "gray" |

#### NOTES
LiteCreditCardInput does not support `requiresName`, `requiresCVC`, and `requiresPostalCode` at the moment, PRs are welcome :party:


## CreditCardInput
| Property | Type | Description |
| --- | --- | --- | --- |
|autoFocus | PropTypes.bool | Automatically focus Card Number field on render|
|onChange | PropTypes.func | Receives a `formData` object every time the form changes |
|onFocus | PropTypes.func | Receives the name of currently focused field |
|labels | PropTypes.object | Defaults to <br/>`{ number: "CARD NUMBER", expiry: "EXPIRY", cvc: "CVC/CCV" }` |
|placeholders | PropTypes.object | Defaults to <br/>`{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" }` |
|cardScale | PropTypes.number | Scales the credit-card view.<br/>Defaults to `1`, which translates to `{ width: 300, height: 190 }` |
|cardFontFamily | PropTypes.string | Font family for the CreditCardView, works best with monospace fonts. Defaults to Courier (iOS) or monospace (android) |
|cardImageFront | PropTypes.number | Image for the credit-card view `e.g. require("./card.png")` |
|cardImageFront | PropTypes.number | Image for the credit-card view `e.g. require("./card.png")` |
|labelStyle | Text.propTypes.style | Style for credit-card form's labels |
|inputStyle | Text.propTypes.style | Style for credit-card form's textInput |
|inputContainerStyle | View.propTypes.style | Style for textInput's container<br/> Defaults to: `{ borderBottomWidth: 1, borderBottomColor: "black" }` |
|validColor | PropTypes.string | Color that will be applied for valid text input. Defaults to: "{inputStyle.color}" |
|invalidColor | PropTypes.string | Color that will be applied for invalid text input. Defaults to: "red" |
|placeholderColor | PropTypes.string | Color that will be applied for text input placeholder. Defaults to: "gray" |
|requiresName | PropTypes.bool | Shows cardholder's name field<br/> Default to `false` |
|requiresCVC | PropTypes.bool | Shows CVC field<br/> Default to `true` |
|requiresPostalCode | PropTypes.bool | Shows postalCode field<br/> Default to `false` |
|validatePostalCode | PropTypes.func | Function to validate postalCode, expects `incomplete`, `valid`, or `invalid` as return values|

# Methods
## setValues
Set values into credit card form


```js
	// sets 4242 on credit card number field
	// other fields will stay unchanged
	this.refs.CCInput.setValues({ number: "4242" });
```

**Known issues:** clearing a field e.g. `setValues({ expiry: "" })` will trigger the logic to `move to previous field` and trigger other kind of weird side effects. **PR plz**


## focus
focus on to specified field

```js
	// focus to expiry field
	this.refs.CCInput.focus("expiry");
```

# Example

In the `example` directory, run:

```bash
npm install

react-native run-ios
# or
react-native run-android
```

# Missing Something? Something is not working?
* Open a GitHub issue, or
* Send a pull request :D
* Make sure `npm run lint` passed

## Contributors

* `Sam Aryasa` ([@sbycrosz](https://github.com/sbycrosz))
* `Alessandro Agosto` ([@lexor90](https://github.com/lexor90))
* `Al` ([@mobiusnz](https://github.com/mobiusnz))
