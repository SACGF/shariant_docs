# API Authentication

The Shariant API will require authentication to perform any operation. The authentication is currently provided through OAuth2 via Keycloak.

The OAuth URL (for production and test) is
`https://shariant.org.au/auth/realms/agha/protocol/openid-connect/token`
provide a client_id of
`shariant-client-tool`

Here's some sample Python code that will be able to login

```python

from requests_oauthlib.oauth2_auth import OAuth2
from requests_oauthlib.oauth2_session import OAuth2Session
from oauthlib.oauth2 import LegacyApplicationClient

def ping() {
	client_id = 'shariant-client-tools'
	username = 'xxxx' #not an actual login, please subsitute with a username and password we've provided you
	password = 'yyyy' 

	oauth = OAuth2Session(client=LegacyApplicationClient(
		client_id=client_id
	))
	token = oauth.fetch_token(
		token_url='https://shariant.org.au/auth/realms/agha/protocol/openid-connect/token',
		username=username,
		password=password,
		client_id=client_id
	)
	auth = OAuth2(client_id = client_id, token = token)

	r = requests.get('https://shariant.org.au:444/variantclassification/api/evidence_keys', auth=auth)
}
```

Note that any classifications you make through the API will be assigned to the user used to authenticate against the API by default.