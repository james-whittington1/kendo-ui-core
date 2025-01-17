---
title: Validate Radio Buttons with Only One Error Message
page_title: Validate Radio Buttons with Only One Error Message | Kendo UI Validator
description: "Learn how to validate radio buttons with only one error message in Kendo UI."
previous_url: /framework/validator/how-to/validate-radio-buttons
slug: howto_validateradiowithonemessage_validator
---

# Validate Radio Buttons with Only One Error Message

The following example demonstrates how to validate a group of Kendo UI radio buttons and show only one error message.

```dojo
<div id="form">
    <span class="k-invalid-msg" data-for="test"></span><br/>
    Test 1<input type="radio" name="test" required /><br/>
    Test 1<input type="radio" name="test" required /><br/>
    Test 1<input type="radio" name="test" required /><br/>
    Test 1<input type="radio" name="test" required /><br/>
    Test 1<input type="radio" name="test" required /><br/>
    <button id="post">Post</button>
</div>

<script>
$(function(){
    var validator = $("#form").kendoValidator({
        rules: {
            radio: function(input) {
                if (input.filter("[type=radio]") && input.attr("required")) {
                    return $("#form").find("[type=radio][name=" + input.attr("name") + "]").is(":checked");
                }
                return true;
            }
        },
        messages: {
            radio: "This is a required field"
        }
    }).getKendoValidator();

    $("#post").click(function() {
        validator.validate();
    });
});
</script>
```

# Validate Radio Buttons with Only One Error Message when the validationSummary is enabled

In scenario when the `validationSummary` is enabled a custom class can be added to the radio inputs. All the items, except one with the specified class needs to be hidden when the validation fails. 

```dojo
<div id="form">
    <div id="summary"></div>
    <span class="k-invalid-msg" data-for="test"></span><br/>
    Test 1<input type="radio" name="test" class="custom" required /><br/>
    Test 1<input type="radio" name="test" class="custom" required /><br/>
    Test 1<input type="radio" name="test" class="custom" required /><br/>
    Test 1<input type="radio" name="test" class="custom" required /><br/>
    Test 1<input type="radio" name="test" class="custom" required /><br/>
    <button id="post">Post</button>
</div>  
<script>
    $(function(){
      var validator = $("#form").kendoValidator({
        validationSummary: {container: '#summary'},
        rules: {
          radio: function(input) {
            if (input.filter("[type=radio]") && input.attr("required")) {
              return $("#form").find("[type=radio][name=" + input.attr("name") + "]").is(":checked");
            }
            return true;
          }
        },
        messages: {
          radio: "This is a required field"
        }
      }).getKendoValidator();      $("#post").click(function() {
        if (validator.validate()) {
          alert("Form completed!");
        }else{		            
          $($('[data-field="test"]').parent()).hide();
          $($('[data-field="test"]')[0]).parent().show()
        }
      });
    });
</script>
```

## See Also

* [Basic Usage of the Validator (Demo)](https://demos.telerik.com/kendo-ui/validator/index)
* [JavaScript API Reference of the Validator](/api/javascript/ui/validator)
