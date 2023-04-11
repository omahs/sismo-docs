---
description: Request proofs from your user on your React project
---

# sismoConnect React: Request

The [sismoConnect](https://docs.sismo.io/sismo-docs/what-is-sismo/sismoconnect) React package is a wrapper of the sismoConnect client package which is a package build on top of the [Sismo Data Vault app](https://docs.sismo.io/sismo-docs/technical-documentation/data-vault-app) (the prover) to easily request proofs from your users.

### Installation

Install the sismoConnect React package in your frontend with `npm` or `yarn`:

```bash
# with npm
npm install @sismo-core/sismo-connect-react
# with yarn
yarn add @sismo-core/sismo-connect-react
```

{% hint style="success" %}
Make sure to have at least v18.15.0 as Node version. You can encounter issues with ethers dependencies if not.
{% endhint %}

## Usage

To integrate sismoConnect into your front end, you can use the sismoConnect button. Clicking on this button will redirect your user to the Sismo Data Vault app, where they can generate their proof.

After your user generates the proof, they will be automatically redirected back to your app with a response containing the generated proof.

<figure><img src="../../.gitbook/assets/sismoConnect.png" alt=""><figcaption><p>sismoConnect button</p></figcaption></figure>

To integrate it you have access through the package to the `SismoConnectButton` component.

```typescript
import { SismoConnectButton, AuthType } from "@sismo-core/sismo-connect-react";

<SismoConnectButton 
    //You will need to register an appId in the Factory
    appId={"0x8f347ca31790557391cec39b06f02dc2"}
    //Request proofs from your users for a groupId
    claimRequest={{
        groupId: "0x42c768bb8ae79e4c5c05d3b51a4ec74a"
    }}
    authRequest={{
        authType: AuthType.ANON
    }}
    messageSignatureRequest={"Your message"}
    //After user redirection get a response containing his proofs 
    onResponse={async (response) => {
        //Send the response to your server to verify proofs
        //thanks to the @sismo-core/sismo-connect-server package
    }}
/>
```

To get the response of your user after his redirection without using the `SismoConnectButton` you can use the `useSismoConnect` hook. This allows you to redirect your user to a page other than the page with the button integrated.

```typescript
import { useSismoConnect, SismoConnectClientConfig } from "@sismo-core/sismo-connect-react";

const config: SismoConnectClientConfig = { appId: "0x8f347ca31790557391cec39b06f02dc2" };

const { response, responseBytes } = useSismoConnect({ config });
```

The `useSismoConnect` hook also exposes the sismoConnect variable which provides access to all the features available in the sismoConnect Client package.

```typescript
const { sismoConnect } = useSismoConnect({ config });
```

Please see the [`sismoConnect Client documentation`](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request) to see all the possibilities around the sismoConnect instance.

### Documentation

This package is a wrapper of the sismoConnect Client package, which means that all the core concepts such as config, claimRequest, authRequest, messageSignatureRequest, and response are the same as in the client package. If you need to explore these concepts in detail, we advise you to refer to the [@sismo-core/sismo-connect-client](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request) page, which provides more detailed information.

#### SismoConnectButton

The SismoConnectButton component will allow you to easily request proofs from your user for a groupId he should be a member of.

```typescript
import { AuthType, SismoConnectButton, SismoConnectClientConfig, SismoConnectResponse } from "@sismo-core/sismo-connect-react";

const config: SismoConnectClientConfig = {
    appId: "0x8f347ca31790557391cec39b06f02dc2", 
    devMode: {
    	// will use the Dev Sismo Data Vault https://dev.vault-beta.sismo.io/
    	enabled: true, 
    	// overrides a group with these addresses
    	devGroups: [{
      		groupId: "0x42c768bb8ae79e4c5c05d3b51a4ec74a",
      		data: {
        		"0x123...abc": 1, 
        		"0x456...efa": 2
      		}
  	}]
    }
};
 
<SismoConnectButton 
    //Request proofs for this groupId
    claimRequest={{
        groupId: "0x42c768bb8ae79e4c5c05d3b51a4ec74a"
    }}
    authRequest={{
        authType: AuthType.ANON
    }}
    messageSignatureRequest={"Your message"}
    config={config}
    onResponse={async (response: SismoConnectResponse) => {
	//Send the response to your server to verify it
	//thanks to the @sismo-core/sismo-connect-server package
    }}
    onResponseBytes={async (bytes: string) => {
           //Send the response to your contract to verify it
           //thanks to the @sismo-core/sismo-connect-solidity package
    }}
/>
```

**Props**

| Prop                                                                  | Type                                                                                                                                            | Description                                                                                                                                                                             |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| appId _(optional but must at least provide this appId or a config)_   | string                                                                                                                                          | appId of your sismoConnect app. Go on the [Sismo Factory](https://factory.sismo.io/apps-explorer) to register your appId.                                                                  |
| claimRequest                                                          | [ClaimRequest](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#claimrequest)                        | The ClaimRequest object holds all the information needed to generate a proof of membership.                                                                                             |
| authRequest                                                           | [AuthRequest](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#authrequest)                          | The AuthRequest object holds all the information needed to generate a proof of account ownership.                                                                                       |
| messageSignatureRequest                                               | string                                                                                                                                          | Message to sign in the vault                                                                                                                                                            |
| config _(optional but must at least provide this config or an appId)_ | [SismoConnectClientConfig](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#sismoconnectclientconfig)      | The config allows you to fully customize your sismoConnect integration.                                                                                                                    |
| verifying _(optional)_                                                | boolean                                                                                                                                         | This prop allows you to trigger the loading of the button.                                                                                                                              |
| onResponse _(optional)_                                               | (response: [SismoConnectResponse](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#getresponse)) ⇒ void | Return a response that contains the proofs generated by your users that must be sent to your backend and verified thanks to the @sismo-core/sismo-connect-server package.                  |
| onResponseBytes (optional)                                            | (bytes: string) => void                                                                                                                         | Return a response in bytes usable in your contracts.                                                                                                                                    |
| callbackPath _(optional)_                                             | string                                                                                                                                          | By default, the redirection will send you back to the same page as your button. The callback path props will send your user to another path. See useSismoConnect to get the user response. |
| overrideStyle                                                         | React.CSSProperties                                                                                                                             | Override style of the sismoConnect                                                                                                                                                         |

**Customization**

If you want to customize the style of your button you can use 3 CSS classes `sismoConnectButton`, `sismoConnectButtonText`, and `sismoConnectButtonLogo`.

An overrideStyle prop is also available on the component which allows you to override the same style as the class sismoConnectButton.

Here is an example of a custom button:

```css
//Added in the index.css of a React app

.sismoConnectButton {
	background: red !important;
}
.sismoConnectButtonText {
	color: blue !important;
}
.sismoConnectButtonLogo {
	display: none
}
```

#### useSismoConnect

The `useSismoConnect` hook makes it easy for you to obtain the response containing the user proof, and it provides access to all functions exposed by the SismoConnect client instance.

```typescript
import { useSismoConnect } from "@sismo-core/sismo-connect-react";

const { sismoConnect, response, responseBytes } = useSismoConnect({ config });
```

**Params**

| Param  | Type                                                                                                                                       | Description                                                                          |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| config | [SismoConnectClientConfig](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#sismoconnectclientconfig) | The SismoConnectClientConfig allows you to fully customize your sismoConnect integration.  |

**States returned**

| State         | Type                                                                                                                                 | Description                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| response      | [SismoConnectResponse](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request#getresponse) \| null | The response contains the proofs generated by your users that must be sent to your backend and verified thanks to the @sismo-core/sismo-connect-server package. |
| responseBytes | string \| null                                                                                                                       | The response contains the proofs generated by your users that must be sent to your contract.                                                                 |
| sismoConnect     | [SismoConnectClient](https://docs.sismo.io/sismo-docs/technical-documentation/sismoconnect/sismoconnect-client-request)                       | SismoConnect instance with the client configuration.                                                                                                            |
