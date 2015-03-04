# SocialLogin
Login social

## Llamar a la libreria en un controlador
$this->load->library('Social');

## Llamar funciones para incorporar login 
<!-- SDK de Face+ -->
<?php echo $this->social->get_social_facebook(); ?>
<!-- SDK de G+ -->
<?php echo $this->social->get_social_gplus(); ?>

## Mostrar botones
<!--Login con Facebook -->
<?php echo $this->social->get_social_facebook_button(); ?>
<!-- Login con G+ -->
<?php echo $this->social->get_social_gplus_button(); ?>


## Libreria Social:

<?php

      /*
      * Para incluir la libreria usar: $this->load->library('Social');
      * Para llamar una funcion usar $this->social->nombre_funcion();
      */

	class Social {
	    private $imprimir;
	    private $url;
	    
	    public function __construct(){
		$this->texto = "";
		$this->url = "";
	    }
	    
	    /*
	    * Esta funcion debe ir dentro del <body>
	    */
	    public function get_social_facebook(){
		 $this->texto = "
		 <div id='fb-root'></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = '//connect.facebook.net/es_LA/sdk.js#xfbml=1&appId=650285908426973&version=v2.0';
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>

		 
	
		<script>

  // This is called with the results from from FB.getLoginStatus().
  function statusChangeCallback(response) {
    console.log('statusChangeCallback');
    console.log(response);
    // The response object is returned with a status field that lets the
    // app know the current login status of the person.
    // Full docs on the response object can be found in the documentation
    // for FB.getLoginStatus().
    if (response.status === 'connected') {
      // Logged into your app and Facebook.
      testAPI();
    } else if (response.status === 'not_authorized') {
      // The person is logged into Facebook, but not your app.
      $('#status').HTML = 'Please log ' +
        'into this app.';
    } else {
      // The person is not logged into Facebook, so we're not sure if
      // they are logged into this app or not.
      $('#status').HTML = 'Please log ' +
        'into Facebook.';
    }
  }
  
  // This function is called when someone finishes with the Login
  // Button.  See the onlogin handler attached to it in the sample
  // code below.
  function checkLoginState() {
    FB.getLoginStatus(function(response) {
      statusChangeCallback(response);
    });
  }

  window.fbAsyncInit = function() {
  FB.init({
    appId      : '650285908426973',
    cookie     : true,  // enable cookies to allow the server to access 
                        // the session
    xfbml      : true,  // parse social plugins on this page
    version    : 'v2.2' // use version 2.2
  });

  // Now that we've initialized the JavaScript SDK, we call 
  // FB.getLoginStatus().  This function gets the state of the
  // person visiting this page and can return one of three states to
  // the callback you provide.  They can be:
  //
  // 1. Logged into your app ('connected')
  // 2. Logged into Facebook, but not your app ('not_authorized')
  // 3. Not logged into Facebook and can't tell if they are logged into
  //    your app or not.
  //
  // These three cases are handled in the callback function.

  //FB.getLoginStatus(function(response) {
    //statusChangeCallback(response);
  //});

  };

  
  // Load the SDK asynchronously
  (function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = '//connect.facebook.net/en_US/sdk.js';
    fjs.parentNode.insertBefore(js, fjs);
  }(document, 'script', 'facebook-jssdk'));

  // Here we run a very simple test of the Graph API after login is
  // successful.  See statusChangeCallback() for when this call is made.
  function testAPI() {
    console.log('Welcome!  Fetching your information.... ');
    FB.api('/me', function(response) {
      console.log('Successful login for: ' + response.name);
      callAjaxData('index.php/Registro_controller', 'dropdown-login', 'html',response.id);
    });
  }
</script>
";

		 return $this->texto;
	    }
	    
	    public function get_social_facebook_button(){
		 $this->texto = "
			<div class='fb-login-button' data-max-rows='1' data-size='medium' data-show-faces='false' data-auto-logout-link='true' onlogin='checkLoginState()'></div>
		 ";
		 return $this->texto; 
	    }
	    
	    public function get_social_twitter(){
		 $this->texto = "Lo borre por mientras";
		 return $this->texto; 
	    }
	    
	    public function get_social_linkedin(){
		  $this->texto = "Lo borre por mientras";
		 return $this->texto;
	    }
	    
	    /*
	    * Esta funcion debe ir dentro del <head>
	    */
	    public function get_social_gplus(){
		  $this->texto = "
		  <script type='text/javascript'>
		    (function() {
		    var po = document.createElement('script'); po.type = 'text/javascript'; po.async = true;
		    po.src = 'https://apis.google.com/js/client:plusone.js';
		    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(po, s);
		  })();
		  </script>
		 
		 <script type='text/javascript'>

 function signinCallback(authResult) {
      if (authResult['status']['signed_in']) {
        // Update the app to reflect a signed in user
        // Hide the sign-in button now that the user is authorized, for example:
        document.getElementById('signinButton').setAttribute('style', 'display: none');
        gapi.client.load('plus', 'v1').then(function() {
        var request = gapi.client.plus.people.get({
              'userId' : 'me'
            });
        request.execute(function(resp) {
              console.log('ID: ' + resp.id);
              console.log('Display Name: ' + resp.displayName);
              console.log('Image URL: ' + resp.image.url);
              console.log('Profile URL: ' + resp.url);
              callAjaxData('index.php/Registro_controller', 'dropdown-login', 'html',resp.id);
            });
            });
      } else {
        // Update the app to reflect a signed out user
        // Possible error values:
        //   'user_signed_out' - User is signed-out
        //   'access_denied' - User denied access to your app
        //   'immediate_failed' - Could not automatically log in the user
        console.log('Sign-in state: ' + authResult['error']);
      }
    }
    
    function logoutGoogle (){
	  gapi.auth.signOut();
    }
    
    </script>
		  ";
		 return $this->texto;
	    }
	    
	    public function get_social_gplus_button(){
		 $this->texto = "
			<span id='signinButton'>
			<span
			  class='g-signin'
			  data-callback='signinCallback'
			  data-clientid='979992688255-hs4amnsa6ntsbkqib5bmna0vvb7tk15i.apps.googleusercontent.com'
			  data-cookiepolicy='single_host_origin'
			  data-requestvisibleactions='http://schemas.google.com/AddActivity'
			  data-scope='https://www.googleapis.com/auth/plus.login https://www.googleapis.com/auth/plus.me'>
			</span>
		      </span>
		 ";
		 return $this->texto; 
	    }
	    
	    
	    
	    public function get_social_all(){
		 $this->texto = "Lo borre por mientras, pero hace un llamado a todas las funciones";
		 return $this->texto;
	    }
	}

?>

