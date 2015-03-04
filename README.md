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

