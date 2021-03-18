jQuery(document).ready(function($) { 
  function checkRedemption() {
    var $gift_container = $('.free-gift--container');

    if ( ! $gift_container.length ) { 
      return;
    }

    var $gift_button    = $gift_container.find('button.free-gift--product'),
        customer_hash   = $gift_button.attr('customer-hash'),
        variant_id      = $gift_button.attr('variant-id');

    if ( customer_hash && variant_id ) { 
      var request_url = '/tools/recurring/portal/' + customer_hash + '/request_objects';
      var added_gift  = false;

      $.ajax({
        url: request_url,
        type: 'get',
        dataType: 'json',
        data: { 
          schema: '{ "orders": { "status": "SUCCESS", "sort_by": "shipped_date-desc" }, "onetimes": [] }' 
        }
      }).done(function(response) {
        var orders   = response.orders,
            onetimes = response.onetimes;

        if ( orders.length ) { 
          for ( var i = 0; i < orders.length; i++ ) {
            for ( var j = 0; j < orders[i].line_items.length; j++ ) {
              if ( variant_id == orders[i].line_items[j].shopify_variant_id ) { 
                added_gift = true;
                break;
              }
            }
          }
        }

        if ( onetimes.length && ! added_gift ) { 
          for ( var i = 0; i < onetimes.length; i++ ) {
            if ( variant_id == onetimes[i].shopify_variant_id ) { 
              added_gift = true;
              break;
            }
          }
        }

        // Update Free Gift top banner
        if ( added_gift ) { 
          $gift_container.find('.free-gift--heading').text('Congrats, your gift is added!');
          $gift_button.hide();
        }
      }).always(function(response) { 
        // console.log(response);
      });
    }

    $gift_container.removeClass('is-loading');
  }

  checkRedemption();

  function addOneTimes($button, product_handle = undefined) { 
    if ( product_handle === undefined ) { 
      return;
    }

    var $form = $('body').find('#Account_NewOneTime');

    if ( window.locked ) { 
      return false; 
    } else { 
      window.locked = true; 
    }

    $.ajax({
      type: 'POST',
      url: $form.attr('action'),
      dataType: 'json',
      data: $form.serialize(),
    }).done(function() {
      $button.find('.text').text('Added!');
      
      if ( $button.hasClass('free-gift--product') ) { 
        $('.free-gift--container .free-gift--heading').text('Congrats, your gift is added!');
        $button.hide();
      }

      Cookies.set('product_handle', product_handle, { expires: 0.1 });

      setTimeout(function(){ 
        window.location.href = $form.find('[name="redirect_url"]').val();
      }, 500);
    }).fail(function(response) {
      $button.find('.text').text('Try again later!');
      $button.addClass('warning').attr('disabled', '');

      delete window.locked;
      return;
    });
  }

  $('body')
    .on('click', '[one-time]', function(e) { 
      var $button          = $(this),
          customer_hash    = $button.attr('customer-hash'),
          variant_id       = $button.attr('variant-id'),
          address_id       = undefined,
          next_charge_date = '',
          product_handle   = $button.attr('product-handle'),
          redirect_url     = '/tools/recurring/login/';

      if ( customer_hash != undefined ) { 
        /** if Customer is a subscriber */

        var base_url      = '/tools/recurring/portal/' + customer_hash + '/',
            request_url   = base_url + 'request_objects',
            onetimes_list = base_url + 'onetimes';

        $.ajax({
          url: request_url,
          type: 'get',
          dataType: 'json',
          data: { schema: '{ "schedule": [] }' }
        }).done(function(response) {
          if ( response.schedule.length ) { 
            address_id = response.schedule[0].orders[0].subscription.address_id;
            next_charge_date = response.schedule[0].date.split('T')[0];

            var form = $('<form action="' + onetimes_list + '" id="Account_NewOneTime" class="visuallyhidden" method="post"></form>');
            $('body').append(form);
            form.append('<input type="hidden" name="redirect_url" value="' + redirect_url + '" />');
            form.append('<input type="hidden" name="purchase_type" value="onetime" />');
            form.append('<input type="hidden" name="shopify_variant_id" value="' + variant_id + '" />');
            form.append('<input type="hidden" name="quantity" value="1" />');
            form.append('<input type="hidden" name="address_id" value="' + address_id + '" />');
            form.append('<input type="hidden" name="next_charge_scheduled_at" value="' + next_charge_date + '" />');
            form.append('<input type="submit" name="submit" value="Submit" />');

            $button.find('.text').text('Processing...');

            addOneTimes($button, product_handle);
          }
        }).always(function(response) { 
          console.log(response);
        });
      }
    })

    .on('change', '.free-gift--product-variants', function(e) { 
      var $selector   = $(this),
          $parent     = $selector.parent(),
          $price      = $selector.find('option:selected').val(),
          $variant_id = $selector.find('option:selected').attr('data-id');

      $parent.find('.free-gift--product-price').text($price);
      $parent.find('.free-gift--product').attr('variant-id', $variant_id);
    })

    .on('click', '[scroll-down]', function(e) { 
      var offset = $('#main-section').offset();
      var header_height = $('#v1-top-nav').height();

      $('body,html').animate({ 
        scrollTop: (offset.top - header_height)
      }, 800);
    });
});