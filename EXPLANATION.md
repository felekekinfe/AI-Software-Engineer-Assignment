# Explanation

### What was the bug?
The `Client.request()` method failed to handle authentication when `self.oauth2_token` was provided as a dictionary. It would skip refreshing expired tokens and fail to attach the `Authorization` header to the request.

### Why did it happen?
The code used `isinstance(self.oauth2_token, OAuth2Token)` as a strict condition to check for expiration and to format the header. Since a dictionary is not an instance of that class, the logic bypassed the authentication block entirely, even though the type hint explicitly allowed dictionaries.

### Why does your fix solve it?
My fix "normalizes" the input. If the token is a dictionary, it immediately converts it into an `OAuth2Token` object. This allows the rest of the existing code to use the `.expired` property and `.as_header()` method without any further changes.

### What’s one realistic case / edge case your tests still don’t cover?
The fix uses dictionary unpacking (`**self.oauth2_token`). If the input dictionary contains extra keys (like a `refresh_token` or `scope` often returned by OAuth providers), the code will crash with a `TypeError` because the `OAuth2Token` dataclass only expects `access_token` and `expires_at`.
