# TikTok OAuth Callback

## Callback URL

`https://masterhollandgamer-png.github.io/humanmaxxed-tiktok-media/auth/tiktok/callback/`

## Purpose

The callback page is the temporary Sandbox redirect destination for the HumanMaxxed TikTok Developer integration. It:

- receives TikTok's OAuth redirect;
- reads the `code`, `state`, `error`, and `error_description` query parameters in the browser;
- displays query-parameter values as text, without interpreting them as HTML;
- does not exchange an authorization code for access or refresh tokens;
- does not automatically transmit the authorization code;
- does not save the code or state to local storage, session storage, cookies, analytics, or external services; and
- does not contain or store a TikTok client secret.

The page may display an authorization code so it can be inspected or copied during Sandbox development. The presence of a code means that TikTok returned an authorization response. It does not mean the TikTok account is fully connected.

## Security boundary

GitHub Pages is public and static. It cannot safely hold a TikTok client secret or perform the confidential authorization-code exchange required to complete OAuth. This callback is suitable as a temporary Sandbox destination, but a secure server-side backend is required before production OAuth is complete.

The callback uses `textContent` for values read from the URL. It does not use `innerHTML` for query-parameter content, log response values, call TikTok's token endpoint, or implement a browser-based substitute for a backend.

## Future server-side implementation

The future backend should:

1. Receive the authorization code.
2. Validate the returned state against the state created for that authorization attempt.
3. Exchange the code through TikTok's official OAuth token endpoint.
4. Store access and refresh tokens securely on the server.
5. Never expose the TikTok client secret to browser code or a public repository.

These server-side steps are intentionally not implemented in this repository.

## Sandbox checks

Success response:

`?code=TEST_CODE&state=TEST_STATE`

Error response:

`?error=access_denied&error_description=Test`

The success URL should display both test values and enable the copy button. The error URL should display the error values as plain text. A URL without a code or error should show the empty-response message and a link back to the HumanMaxxed homepage.

