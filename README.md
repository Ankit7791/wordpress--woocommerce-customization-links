# wordpress--woocommerce-customization-links

//elementor pro plugin wp-content/plugins/elementor-pro/modules/woocommerce/module.php if any fatalerror

		if ( isset( $settings['posts_per_page'] ) && isset( $settings['columns'] ) ) {
			$settings['rows'] = ceil( $settings['posts_per_page'] / $settings['columns'] );
		}
		

Change on 1543 Line to this   
	
	if (isset($settings['posts_per_page']) && isset($settings['columns'])) {
	    $settings['rows'] = ceil((int) $settings['posts_per_page'] / (int) $settings['columns']);
	}

//jetengine macros
https://crocoblock.com/knowledge-base/articles/jetengine-macros-guide/

//custom post type archieve page with load more ajax functionality
https://weichie.com/blog/load-more-posts-ajax-wordpress/
https://rudrastyh.com/wordpress/load-more-posts-ajax.html

//create custom payment gateway
https://www.skyverge.com/blog/how-to-create-a-simple-woocommerce-payment-gateway/

//show attribute name on single product page via shortcode
https://stackoverflow.com/questions/39394127/woocommerce-display-single-product-attributes-with-shortcodes-in-frontend

//To find where in wordpress the menu items are stored 
https://digitalzoomstudio.net/2017/07/31/where-to-find-menus-in-wordpress-database/

//create your custom post type gallery using lightslider
https://wpbeaches.com/image-carousel-thumbnail-slider-acf-gallery-field-wordpress/?__cf_chl_captcha_tk__=3a90d5e30deac1b57364238bb39a9bab5660af1f-1597835785-0-AR29VBNW4JLEFGxfnBWV6d0tHniV10rY0nOPblhfWdAs5-o_ZgbODmMJOn4C_vF7cyUVD5_YVzjWjvnm5kwSlAM7SxRv6Mn9rroHzVxOryq4QbApQ52Mw3WTSytlPuW9EoTapHOQVU5dxJCIpP2oiaudycciopAuSGidOQwm5QPKoAKwHTovfxyTbPGa3qi-6E5vSZd0E9zynfj3IGUg2PrBlbVp8ogNB3kAc5OonsEBoTMO3K6a10Gi7s3doGxTf3hBJLbuBoFi_OmKvku6UQuna-Lj9I81aUAqSV9q9CWaMaxnA_hc44RWftXStraECGf_uBiEXWi3R-ev8Yn6kijSh0xz2HcX8a1MWqfHRWIrx-Prjslk9gPkbrhc6h_7Yhipn1ai9RcVU7MK2UPaunhltqOYQe_tWOjkBz2M2pCOe4Uc9p_WA4njHErgJxQLoQNzSoRwYWcStC00vBEAaK_bSWs_77MDVZG7fm8fRCuP7JcYZw7eaIE1O6vdPD2V22o0iORlKUHaktO9kooTwMf7yPhmdBv8jM3UJHVBh5vFdo5U7ovMm2R39oB0zuG1uQ

//show product taxes and calculation on cart page 
https://stackoverflow.com/questions/51357197/get-tax-rate-separately-for-every-cart-and-order-items-in-woocommerce

		 <td class="product-subtotal" data-title="<?php esc_attr_e( 'Total', 'woocommerce' ); ?>">
                            <?php
                                echo apply_filters( 'woocommerce_cart_item_subtotal', WC()->cart->get_product_subtotal( $_product, $cart_item['quantity'] ), $cart_item, $cart_item_key ); // PHPCS: XSS ok.
                            ?>
                            
                            <?php
                                echo '<br/>';
							    $tax_name = apply_filters( 'woocommerce_cart_item_tax', $_product->get_tax_class(), $cart_item, $cart_item_key );
                                           
                                echo "  ".$cart_item['line_subtotal_tax']." ل.ل (".$tax_rate."VAT)";
							?>
							
							<?php 
							    
							      echo "<br/> -------------------- <br/>";
							     $ctotal = apply_filters( 'woocommerce_cart_item_subtotal', WC()->cart->get_product_subtotal( $_product, $cart_item['quantity'] ), $cart_item, $cart_item_key );
							     
							     $stotal = explode(' ',$ctotal);
							     $sbtotal = explode('>',$stotal[2]);
							     //print_r($sbtotal[1]);
							     $taxes = $cart_item['line_subtotal_tax'];
							     
							     $number = (float) str_replace(',', '', $sbtotal[1]);
							     
							     $ftotal = $taxes+$number;
							     
							     
							     echo " ".$ftotal. " ل.ل 
							      (Total)"
							
							?>
							
                        </td>



//editing the woocommerce lottery plugin to show the current count of the tickets purchased 

        global $wpdb; 
        $result = $wpdb->get_results("SELECT count(ticket_number) as ticket FROM `carparts_wc_lottery_pn_log` where lottery_id = $lotteryid"); 
        if($result[0]->ticket > 0){
            return $result[0]->ticket;
        }


//How to prevent non-buyers from reviewing your WooCommerce products

https://barn2.com/woocommerce-allow-reviews-verified-buyers/

//customize myaccount pages 
https://www.youtube.com/watch?v=iEfrFSTPCSQ&t=1243s

//woocommerce get lowest price in category

	function wpq_get_min_price_per_product_cat( $term_id ) {
	  global $wpdb;
	  $sql = "
	    SELECT  MIN( meta_value+0 ) as minprice
	    FROM {$wpdb->posts} 
	    INNER JOIN {$wpdb->term_relationships} ON ({$wpdb->posts}.ID = {$wpdb->term_relationships}.object_id)
	    INNER JOIN {$wpdb->postmeta} ON ({$wpdb->posts}.ID = {$wpdb->postmeta}.post_id) 
	    WHERE  
	      ( {$wpdb->term_relationships}.term_taxonomy_id IN (%d) ) 
	    AND {$wpdb->posts}.post_type = 'product' 
	    AND {$wpdb->posts}.post_status = 'publish' 
	    AND {$wpdb->postmeta}.meta_key = '_price'
	    AND {$wpdb->postmeta}.meta_value != 'outofstock'

	  ";
	  return $wpdb->get_var( $wpdb->prepare( $sql, $term_id ) );
	}
	add_filter('custom_lowest_pricing_category', 'wpq_get_min_price_per_product_cat');

//Wordpress Security to be added in .htaccess

	<ifModule mod_headers.c>
	Header set Strict-Transport-Security "max-age=31536000" env=HTTPS
	Header set X-XSS-Protection "1; mode=block"
	Header set X-Content-Type-Options nosniff
	Header set X-Frame-Options DENY
	Header set Referrer-Policy: no-referrer-when-downgrade
	</ifModule>
	
//wordpress hack, remove .htaccess file from all folders , run this command in terminal 

	find / -name "*.htaccess" -type f (this command finds and show list of htaccess files)
	find -name ".htaccess" -type f -delete (deletes all the htaccess files)


//How to fix wrong price sorting and filters in woocommerce
https://wpsoul.com/how-to-fix-wrong-price-sorting-and-filters-in-woocommerce/


	add_filter('woocommerce_get_catalog_ordering_args', function ($args) {
    $orderby_value = isset($_GET['orderby']) ? wc_clean($_GET['orderby']) : apply_filters('woocommerce_default_catalog_orderby', get_option('woocommerce_default_catalog_orderby'));

    if ('price' == $orderby_value) {
        $args['orderby'] = 'meta_value_num';
        $args['order'] = 'ASC';
        $args['meta_key'] = '_price';
    }

    if ('price-desc' == $orderby_value) {
        $args['orderby'] = 'meta_value_num';
        $args['order'] = 'DESC';
        $args['meta_key'] = '_price';
    }

    return $args;
});


#Add to cart hide and role specific
	
	// Replacing the button add to cart by a link to the product in Shop and archives pages
add_filter( 'woocommerce_loop_add_to_cart_link', 'replace_loop_add_to_cart_button', 10, 2 );
function replace_loop_add_to_cart_button( $button, $product  ) {
    // Only for logged in users
    if( ! is_user_logged_in() ) 
	{
    $button_text = __( "View product", "woocommerce" );
    $button = '<a class="button" href="' . $product->get_permalink() . '">' . $button_text . '</a>';

    return $button;
	}else{

                $user = wp_get_current_user();
		if ( in_array( 'fieldtesters_france', (array) $user->roles ) || in_array( 'fieldtester', (array) $user->roles )
		|| in_array( 'fieldtesters_spain', (array) $user->roles ) || in_array( 'promo_team', (array) $user->roles || in_array( 'administrator', (array) $user->roles )  )
		 ) {

                         $button_text = __( "Add to Cart", "woocommerce" );
    $button = '<a class="button" href="' . $product->get_permalink() . '">' . $button_text . '</a>';

return $button;


		}else{

                         $button_text = __( "View product", "woocommerce" );
    $button = '<a class="button" href="' . $product->get_permalink() . '">' . $button_text . '</a>';

    return $button;
                }
        }
}


add_action( 'woocommerce_single_product_summary', 'remove_add_to_cart_button', 1 );
function remove_add_to_cart_button() {
    // Only for logged in users
    if( ! is_user_logged_in() ) {

			//The user has the "author" role
			global $product;

			// For variable product types (keeping attribute select fields)
			if( $product->is_type( 'variable' ) ) {
				remove_action( 'woocommerce_single_variation', 'woocommerce_single_variation_add_to_cart_button', 20 );
			}
			// For all other product types
			else {
				remove_action( 'woocommerce_single_product_summary', 'woocommerce_template_single_add_to_cart', 30 );;
			}
		}

	else {

		$user = wp_get_current_user();
		if ( in_array( 'fieldtesters_france', (array) $user->roles ) || in_array( 'fieldtester', (array) $user->roles )
		|| in_array( 'fieldtesters_spain', (array) $user->roles ) || in_array( 'promo_team', (array) $user->roles ) || in_array( 'administrator', (array) $user->roles )
		 ) {


		}else{
			//The user has the "author" role
			global $product;

			// For variable product types (keeping attribute select fields)
			if( $product->is_type( 'variable' ) ) {
				remove_action( 'woocommerce_single_variation', 'woocommerce_single_variation_add_to_cart_button', 20 );
			}
			// For all other product types
			else {
				remove_action( 'woocommerce_single_product_summary', 'woocommerce_template_single_add_to_cart', 30 );;
			}
		}
	}
}

add_action( 'woocommerce_product_meta_start','content_after_addtocart', 100 );
  function content_after_addtocart() {
  // place your content below.

   if( ! is_user_logged_in() ) {
  			echo 'Please <a href="https://www.urbanbait.co.uk/my-account">login</a> to Order <br/> <br/>';
   }else{

	   $user = wp_get_current_user();
		if ( in_array( 'fieldtesters_france', (array) $user->roles ) || in_array( 'fieldtester', (array) $user->roles )
		|| in_array( 'fieldtesters_spain', (array) $user->roles ) || in_array( 'promo_team', (array) $user->roles ) || in_array( 'administrator', (array) $user->roles )
		 ) {

		}else{

			echo 'Your are not allowed to order <br/> ';

		}
   }
}

