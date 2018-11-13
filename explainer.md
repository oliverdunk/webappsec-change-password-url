## Explainer

Currently, if the user of a password manager would like to change their
password on `example.com`, basically all the password manager can do is
load `example.com` in a browser tab and hope the user can figure out how
to update their password themselves.

The goal of [this spec](index.html) is to do the simplest
possible thing to improve this situation.

### Proposal

`example.com` provides a `/.well-known/change-password` resource which
redirects to their change password form, wherever it happens to already
be.

Password managers check for the existence of
`/.well-known/change-password` on `https://example.com`.

If it's there (the response code is `2xx` or `3xx`), the password
manager can cause the user's browser to navigate there when the user
indicates they'd like to change their password.

That's it, really. It's a pretty simple idea.

### Frequently Asked Questions

#### Why not allow sites to override this location with an HTTP Link header or an HTML `link` element?

Implementation complexity. (This would require keeping site-specific state client-side, verifying &
invalidating said state periodically, etc.)

#### Why not serve a JSON resource with links to other account management functions?

Specification complexity. If we determine we need other account
management well-known resources in the future, we can specify them then.

#### What tools have implemented this feature?

* iCloud Keychain on iOS 12
* Safari 12