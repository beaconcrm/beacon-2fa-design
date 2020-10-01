# beacon-2fa-design

## Background

At Beacon, we've implemented two-factor authentication (2FA) to help keep user accounts secure. Our customers our charities storing huge amounts of sensitive data, so it's really important that as many of them enable 2FA as possible.

To help encourage this, we want to build a feature to **encourage** (not force) them to enable 2FA when they login.

## Current implementation

### User experience

1. User logs in
2. If 2FA is enabled, prompt them to enter a code (from Authy or Google Authenticator) to fully login.
3. If 2FA is not enabled, login immediately.

### Database

We use a PostgreSQL database to store users, and many other tables.

The `users` table is structured like this:

| id | email | is_two_factor_enabled | two_factor_secret |
| ---|-------|-----------------------|-------------------|
| 1  | chris@beaconcrm.org | false | null |
| 2  | david@beaconcrm.org | true | abc12312312abc |


## Your task

As mentioned above, we want to encourage users who don't have 2FA enabled to enable it when they are logging in.

However - we __don't__ want to encourage them to enable 2FA on _every single login_. We'd like to encourage them to enable it __no more than once every 7 days__.

To make this possible, we'd like you to design:

1. A new API endpoint to check if the user should be encouraged to enable 2FA
2. Some changes to the `users` table, or an entirely new table if you prefer (the API endpoint should use this)
3. A new page 
