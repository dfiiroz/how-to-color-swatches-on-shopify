# how-to-add-color-swatches-on-shopify
How to Add Color Swatches on Shopify
How to add color swatches to Shopify 

Step 1: 
Go to your shopify admin dashboard 
Now click on Online Store
Now you’ll see your default shopify theme (Debut) If you’re new.
Link example: https://yourstorename.myshopify.com/admin/themes


Step 2: 
Now Click On Action
Now Click on Edit Code


Step 3: 
Go to Template Folder
Then Click on product.liquid

Now you’ll see {% section 'product-template' %}

Step 4: 
Go to section folder
Click on product-template.liquid

Now Press CTRL + F

Search keyword “unless”
Now you’ll see 

            {% unless product.has_only_default_variant %}
              <div class="product-form__controls-group">
                {% for option in product.options_with_values %}
                  <div class="selector-wrapper js product-form__item">
                    <label for="SingleOptionSelector-{{ forloop.index0 }}">
                      {{ option.name }}
                    </label>
                    <select class="single-option-selector single-option-selector-{{ section.id }} product-form__input"
                      id="SingleOptionSelector-{{ forloop.index0 }}"
                      data-index="option{{ forloop.index }}"
                    >
                      {% for value in option.values %}
                        <option value="{{ value | escape }}"{% if option.selected_value == value %} selected="selected"{% endif %}>{{ value }}</option>
                      {% endfor %}
                    </select>
                    {% if product.available and product.variants.size > 1 %}
                    {% render 'swatch' for product.options as swatch %}
                    {% endif %} 
                    {% include 'color-swatch' %} 
                  </div>
                {% endfor %}
              </div>
            {% endunless %}


And now you have to replace the code as below

{% unless product.has_only_default_variant %}
<div class="product-form__controls-group">
  {% for option in product.options_with_values %}
    <div class="selector-wrapper js product-form__item">
 
      {% if option.name == "Color" %}
        <label for="">{{ option.name }}</label>
        {% assign index = forloop.index%}
 
        <div class="firoz_color_swatches">
        {% for value in option.values %}
        <input class="single-option-selector-{{ section.id }}" id="color-{{ forloop.index }}" type="radio" name="Color" value="{{ value | escape }}" data-index="option{{                   index }}" {% if option.selected_value == value %}checked{% endif %}/>
          <label for="color-{{ forloop.index }}">
            <img src="{{ value | escape | downcase | append: '.png' | strip | asset_url }}" alt="">
          </label>
        {% endfor %}
      </div>  
      {% else %}
      <label {% if option.name == 'default' %}class="label--hidden"{% endif %} for="SingleOptionSelector-{{ forloop.index0 }}">
        {{ option.name }}
      </label>
 
        <select class="single-option-selector single-option-selector-{{ section.id }} product-form__input"
        id="SingleOptionSelector-{{ forloop.index0 }}"
        data-index="option{{ forloop.index }}"
        >
        {% for value in option.values %}
          <option value="{{ value | escape }}"{% if option.selected_value == value %} selected="selected"{% endif %}>{{ value }}</option>
        {% endfor %}
        </select>
      {% endif %}
 
    </div>
  {% endfor %}
</div>
{% endunless %}



Final Step: 

Add the piece of CSS code from below on your theme.css or theme.scss.liquid file in assets folder

/* Custom Color Swatches CSS */
 
.firoz_color_swatches {
  display: flex;
  justify-content: space-between;
}
.firoz_color_swatches input {
  display: none;
}
.firoz_color_swatches label {
  max-height: 44px;
  margin-right: 5%;
}
.firoz_color_swatches label:last-child {
  margin-right: 0%;
}
.firoz_color_swatches img {
  width: 100%;
  height: 100%;
  border: 3px solid #d6d5d5;
  /* border-radius: 50%; */
}
 
.firoz_color_swatches input:checked + label {
  border: 2px solid black;
}


Now have to do the last task, you have to make images screenshots of dimension as 50x50px and use windows paint tool or figma  and name those as blue.png or black.png whatever color of variants you added on your product listing time and upload those pictures to the assets folder.

Congratulations. You have done the color swatches successfully.

Best Regards,
Firoz Hossain
