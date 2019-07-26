# GoAPIWithUnitTesting

1st Step: create a variable which is assigned to anonymous function which retuns response & error
        # In GoApi.go instead of line 33, create dependencies() at line 34.
        
      1)  reponse, err := dependencies()
      2) var dependencies = func() (*http.Response, error) {
	                   return http.Get("https://httpbin.org/get")
                      }
        
2nd Step: create a mock variable (in GoApi_test.go)which is assigned to anonymous function which retuns mockresponse & mockerror.
         
         dependencies = func() (*http.Response, error) {
		return &http.Response{}, http.ErrShortBody
	}   
  
  3rd Step : Depending on test scenario , change the the mock response in mock variable.
             eg:
             # GetPersonStatusBadGateway
                change mock dependencies rturn http.response as &http.Response{}, http.ErrShortBody.
                
             # GetPersonStatusNotFound
               change mock dependencies rturn &http.Response{}, nil.
             # GetPersonHappyPath
               change mock dependencies return &http.Response{Status: "OK", StatusCode: 200, Body: ioutil.NopCloser(bytes.NewBufferString(`OK`))}, nil
