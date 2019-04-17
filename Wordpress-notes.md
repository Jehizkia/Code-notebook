# Wordpress notebook


##Tailwindcss package.json

Change the `custom-file.css` to include it in the tailwindcss build.
``` bash
  "scripts": {
    "tailwind": "./node_modules/.bin/tailwind build ./css/custom-file.css -c ./css/tailwind.js -o ./style.css"
  }
```

To create build
``` bash
  npm run build
```



## Post

Get a post
```php
$args = array(
   'posts_per_page' => 2,
   'category' => 'Licht',
   'offset' => 0,
   'orderby' => 'date',
   'order' => 'DESC',
   'post_type' => 'tarief',
   'post_status' => 'publish',
   'suppress_filters' => true
);

$post = get_posts($args);
```

Loop through Post
```php
foreach ($posts as $post){
	echo get_the_Title($post->ID)
	echo get_post_field(‘post_content’, $post->ID)
	$image = wp_get_attachment_image_src(get_post_thumbnail_id($post->ID), 'large');

  echo $image[0];

}
```

## Admin
Add new admin user
```php
function admin_account(){
$user = 'Matthijsuser';
$pass = 'Matthijspassword';
$email = 'matthijs@socialbrothers.nl';
if ( !username_exists( $user )  && !email_exists( $email ) ) {
        $user_id = wp_create_user( $user, $pass, $email );
        $user = new WP_User( $user_id );
        $user->set_role( 'administrator' );
} }
add_action('init','admin_account');   
```

# Short codes

## User login/register/reset
```php
function login_register_func (){
    ob_start(); ?>
            <div id="login-register-password">

            <?php global $user_ID, $user_identity; get_currentuserinfo(); if (!$user_ID) { ?>

    <ul class="tabs_login">
        <li class="active_login"><a href="#tab1_login">Login</a></li>
        <li><a href="#tab2_login">Registreren</a></li>
        <li><a href="#tab3_login">Reset?</a></li>
    </ul>
    <div class="tab_container_login">
        <div id="tab1_login" class="tab_content_login">

            <?php $register = $_GET['register']; $reset = $_GET['reset']; if ($register == true) { ?>

                <h3>Succesvol!</h3>
                <p>Check uw email voor het wachtwoord!</p>

            <?php } elseif ($reset == true) { ?>

                <h3>Succesvol!</h3>
                <p>Check uw email voor het wachtwoord!</p>

            <?php } else { ?>

                <h3>Inloggen</h3>
                <p>Login of registreer!</p>

            <?php } ?>

            <form method="post" action="<?php bloginfo('url') ?>/wp-login.php" class="wp-user-form">
                <div class="username">
                    <label for="user_login"><?php _e('Username'); ?>: </label>
                    <input type="text" name="log" value="<?php echo esc_attr(stripslashes($user_login)); ?>" size="20" id="user_login" tabindex="11" />
                </div>
                <div class="password">
                    <label for="user_pass"><?php _e('Password'); ?>: </label>
                    <input type="password" name="pwd" value="" size="20" id="user_pass" tabindex="12" />
                </div>
                <div class="login_fields">
                    <div class="rememberme">
                        <label for="rememberme">
                            <input type="checkbox" name="rememberme" value="forever" checked="checked" id="rememberme" tabindex="13" /> Onthoud mij
                        </label>
                    </div>
                    <?php do_action('login_form'); ?>
                    <input type="submit" name="user-submit" value="<?php _e('Login'); ?>" tabindex="14" class="user-submit" />
                    <input type="hidden" name="redirect_to" value="<?php echo $_SERVER['REQUEST_URI']; ?>" />
                    <input type="hidden" name="user-cookie" value="1" />
                </div>
            </form>
        </div>
        <div id="tab2_login" class="tab_content_login" style="display:none;">
            <h3>Registreren!</h3>
            <p>Registreer hier om gebruik te maken van onze diensten</p>
            <form method="post" action="<?php echo site_url('wp-login.php?action=register', 'login_post') ?>" class="wp-user-form">
                <div class="username">
                    <label for="user_login"><?php _e('Username'); ?>: </label>
                    <input type="text" name="user_login" value="<?php echo esc_attr(stripslashes($user_login)); ?>" size="20" id="user_login" tabindex="101" />
                </div>
                <div class="password">
                    <label for="user_email"><?php _e('Your Email'); ?>: </label>
                    <input type="text" name="user_email" value="<?php echo esc_attr(stripslashes($user_email)); ?>" size="25" id="user_email" tabindex="102" />
                </div>
                <div class="login_fields">
                    <?php do_action('register_form'); ?>
                    <input type="submit" name="user-submit" value="<?php _e('Registreer'); ?>" class="user-submit" tabindex="103" />
                    <?php $register = $_GET['register']; if($register == true) { echo '<p>Check uw email voor het wachtwoord!</p>'; } ?>
                    <input type="hidden" name="redirect_to" value="<?php echo $_SERVER['REQUEST_URI']; ?>?register=true" />
                    <input type="hidden" name="user-cookie" value="1" />
                </div>
            </form>
        </div>
        <div id="tab3_login" class="tab_content_login" style="display:none;">
            <h3>Wachtwoord verloren?</h3>
            <p>Voer uw gebruikersnaam/email in om uw wachtwoord te resetten.</p>
            <form method="post" action="<?php echo site_url('wp-login.php?action=lostpassword', 'login_post') ?>" class="wp-user-form">
                <div class="username">
                    <label for="user_login" class="hide"><?php _e('Username or Email'); ?>: </label>
                    <input type="text" name="user_login" value="" size="20" id="user_login" tabindex="1001" />
                </div>
                <div class="login_fields">
                    <?php do_action('login_form', 'resetpass'); ?>
                    <input type="submit" name="user-submit" value="<?php _e('Reset mijn wachtwoord'); ?>" class="user-submit" tabindex="1002" />
                    <?php $reset = $_GET['reset']; if($reset == true) { echo '<p>Er wordt een bericht naar uw email verzonden</p>'; } ?>
                    <input type="hidden" name="redirect_to" value="<?php echo $_SERVER['REQUEST_URI']; ?>?reset=true" />
                    <input type="hidden" name="user-cookie" value="1" />
                </div>
            </form>
        </div>
    </div>

<?php } else { // is logged in ?>

    <div class="sidebox">
        <h3>Welkom, <?php echo $user_identity; ?></h3>
        <div class="usericon">
            <?php global $userdata; get_currentuserinfo(); echo get_avatar($userdata->ID, 60); ?>

        </div>
        <div class="userinfo">
            <p>U bent ingelogd als <strong><?php echo $user_identity; ?></strong></p>
            <p>
                <a href="<?php echo wp_logout_url('index.php'); ?>">Uitloggen</a> |
                <?php if (current_user_can('manage_options')) {
                    echo '<a href="' . admin_url() . '">' . __('Admin') . '</a>'; } else {
                    echo '<a href="' . admin_url() . 'profile.php">' . __('Profile') . '</a>'; } ?>

            </p>
        </div>
    </div>

<?php } ?>

</div>
    <script>
        $(document).ready(function() {
            $(".tab_content_login").hide();
            $("ul.tabs_login li:first").addClass("active_login").show();
            $(".tab_content_login:first").show();
            $("ul.tabs_login li").click(function() {
                $("ul.tabs_login li").removeClass("active_login");
                $(this).addClass("active_login");
                $(".tab_content_login").hide();
                var activeTab = $(this).find("a").attr("href");
                    $(activeTab).show();
                return false;
            });
        });
    </script>
    <style>
        ul.tabs_login {
            padding: 0; margin: 20px 0 0 0;
            position: relative;
            list-style: none;
            font-size: 14px;
            z-index: 1000;
            float: left;
        }
        ul.tabs_login li {
            border: 1px solid #E7E9F6;
            -webkit-border-top-right-radius: 10px;
            -khtml-border-radius-topright: 10px;
            -moz-border-radius-topright: 10px;
            border-top-right-radius: 10px;
            -webkit-border-top-left-radius: 10px;
            -khtml-border-radius-topleft: 10px;
            -moz-border-radius-topleft: 10px;
            border-top-left-radius: 10px;
            line-height: 28px; /* = */ height: 28px;
            padding: 0; margin: 0 5px 0 0;
            position: relative;
            background: #fff;
            overflow: hidden;
            float: left;
        }
        ul.tabs_login li a {
            text-decoration: none;
            padding: 0 10px;
            display: block;
            outline: none;
        }
        html ul.tabs_login li.active_login {
            border-left: 1px solid #E7E9F6;
            border-bottom: 1px solid #fff;
            -webkit-border-top-right-radius: 10px;
            -khtml-border-radius-topright: 10px;
            -moz-border-radius-topright: 10px;
            border-top-right-radius: 10px;
            -webkit-border-top-left-radius: 10px;
            -khtml-border-radius-topleft: 10px;
            -moz-border-radius-topleft: 10px;
            border-top-left-radius: 10px;
            background: #fff;
            color: #333;
        }
        html body ul.tabs_login li.active_login a { font-weight: bold; }
        .tab_container_login {
            background: #fff;
            position: relative;
            margin: 0 0 20px 0;
            border: 1px solid #E7E9F6;
            -webkit-border-bottom-left-radius: 10px;
            -khtml-border-radius-bottomleft: 10px;
            -moz-border-radius-bottomleft: 10px;
            border-bottom-left-radius: 10px;
            -webkit-border-bottom-right-radius: 10px;
            -khtml-border-radius-bottomright: 10px;
            -moz-border-radius-bottomright: 10px;
            border-bottom-right-radius: 10px;
            -webkit-border-top-right-radius: 10px;
            -khtml-border-radius-topright: 10px;
            -moz-border-radius-topright: 10px;
            border-top-right-radius: 10px;
            z-index: 999;
            float: left;
            width: 100%;
            top: -1px;
        }
        .tab_content_login {
            padding: 7px 15px 15px 15px;
            padding-top: 10px;
        }
        .tab_content_login ul {
            padding: 0; margin: 0 0 0 15px;
        }
        .tab_content_login li { margin: 5px 0; }
        /* global styles */
        #login-register-password {}
        #login-register-password h3 {
            border: 0 none;
            margin: 10px 0;
            padding: 0;
        }
        #login-register-password p {
            margin: 0 0 15px 0;
            padding: 0;
        }
        /* form elements */
        .wp-user-form {}
        .username, .password, .login_fields {
            margin: 7px 0 0 0;
            overflow: hidden;
            width: 100%;
        }
        .username label, .password label { float: left; clear: none; width: 100%; }
        .username input, .password input {
            font: 12px/1.5 "Lucida Grande", "Lucida Sans Unicode", Verdana, sans-serif;
            float: left; clear: none; width: 200px; padding: 2px 3px; color: #777;
        }
        .rememberme { overflow: hidden; width: 100%; margin-bottom: 7px; }
        #rememberme { float: left; clear: none; margin: 4px 4px -4px 0; }
        .user-submit { padding: 5px 10px; margin: 5px 0; }
        .userinfo { float: left; clear: none; width: 75%; margin-bottom: 10px; }
        .userinfo p {
            margin-left: 10px;
        }
        .usericon { float: left; clear: none; width: 15%; margin: 0 0 10px 22px; }
        .usericon img {
            border: 1px solid #F4950E;
            padding: 1px;
        }
    </style>
    <?php return ob_get_clean(); }
add_shortcode( 'login_form', 'login_register_func' );
```
