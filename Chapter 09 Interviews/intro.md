What is a request:

    request.body              # request body sent by the client (see below)
    request.scheme            # "http"
    request.script_name       # "/example"
    request.path_info         # "/foo"
    request.port              # 80
    request.request_method    # "GET"
    request.query_string      # ""
    request.content_length    # length of request.body
    request.media_type        # media type of request.body
    request.host              # "example.com"
    request.get?              # true (similar methods for other verbs)
    request.form_data?        # false
    request.referer           # the referer of the client or '/'
    request.user_agent        # user agent (used by :agent condition)
    request.cookies           # hash of browser cookies
    request.xhr?              # is this an ajax request?
    request.url               # "http://example.com/example/foo"
    request.path              # "/example/foo"
    request.ip                # client IP address
    request.secure?           # false


What do you get as a response:



More on requests and responses:

http://www.jmarshall.com/easy/http/#headmethod