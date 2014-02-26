rest-script
===========

A script for issuing sequences of RESTful calls.

Example:


    // Define defaults
    Defaults:
      Root: http://api.example.com                    // The root of the API
      Request-Header: Accept: application/json        // Tell API to send Json
      Expect-Header: Content-Type: application/json   // Fail if the retrieved content is not Json
      Expect-Status: OK                               // Expect all calls to response with OK ( could also type 200)
      
    // Call the root, typically containing links to other resources
    Send: GET /
    
    // Read out a Json property, in this case the link to the users collection resource
    $usersLink = Json._links.users
    
    // Get the retrived link
    Send: GET $usersLink
    
    // Read a Json template and complete the template
    $userTemplate = json->json._links.user
    $userLink = Complete-Template $userTemplate {id: 4} 
    
    Send GET $userLink
    
    $userName = Json.name
    
    Print: $userName
    
    ----------------
    
    Send: GET /
    
    $commentsLink = Json._links.comments
    
    Send: POST $commentsLink
      Header Content-Type: application/json
      BeginBody """
      {
        "text": "$user is awesom!"
      }
      """l
      Expect-Status Created
      Expect-Header Location
    
    
    
    
    
    
