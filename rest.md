# -*- restclient -*-
# Testing Restclient against TinyTiny RSS API
# Variables
# Load TTRSS Password from lastpass
:TTRSS_PASS := (lastpass-getpass "lahtela.me")
:API = https://lahtela.me/tt/api/
#    C-c C-c: runs the query under the cursor, tries to pretty-print the response (if possible)
#    C-c C-p: jump to the previous query
#    C-c C-n: jump to the next query
#    C-c C-.: mark the query under the cursor
#    C-c C-u: copy query under the cursor as a curl command
#    C-c C-g: start a helm session with sources for variables and requests (if helm is available, of course)
#    C-c C-i: show information on resclient variables at point


# Login
# Save Session id to SID
POST :API
-> jq-set-var :SID .content.session_id
Content-Type: application/json

{"op":"login","user":"admin","password":":TTRSS_PASS"}


# GET Categories
# Use SID from above
POST :API

{"sid":":SID","op":"getCategories"}

# Feed tree
POST :API

{ "sid":":SID", "op": "getFeedTree"}