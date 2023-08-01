<?php
$current_product_id = get_the_ID();
$current_product_categories = wp_get_post_terms($current_product_id, 'product_cat');

if (!empty($current_product_categories)) {
    $current_category_id = $current_product_categories[0]->term_id;

    // Filter related products to include only products from the same category as the current product
    $related_products_filtered = array_filter($related_products, function($related_product) use ($current_category_id) {
        $related_product_categories = wp_get_post_terms($related_product->get_id(), 'product_cat');
        return !empty($related_product_categories) && $related_product_categories[0]->term_id === $current_category_id;
    });

    foreach ($related_products_filtered as $related_product) :
        $post_object = get_post($related_product->get_id());
        setup_postdata($GLOBALS['post'] =& $post_object);
        $style = liquid_helper()->get_option('wc-archive-product-style');
?>

        <div class="prod_cat"><?php echo esc_html($current_product_categories[0]->name); ?></div>

        <?php
        if ('minimal' === $style || 'minimal-2' === $style) {
            wc_get_template_part('content', 'product-minimal');
        } elseif ('minimal-hover-shadow' === $style) {
            wc_get_template_part('content', 'product-minimal-hover-shadow');
        } elseif ('minimal-hover-shadow-2' === $style) {
            wc_get_template_part('content', 'product-minimal-hover-shadow-2');
        } else {
            wc_get_template_part('content', 'product');
        }
        ?>

    <?php endforeach;
} ?>
