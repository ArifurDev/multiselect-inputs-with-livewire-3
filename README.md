# Using Multiselect Inputs with Livewire 3

This guide explains how to implement multiselect inputs with Livewire 3.

## Blade Template
### (resources/views/livewire/your-component.blade.php)

Add the following Blade code to your view. The `wire:ignore` directive is used to prevent Livewire from interfering with the jQuery plugin.

```blade
<div class="form-group" wire:ignore>
        <label for="options">Select Options:</label>
        <select class="form-control mb-3 js-example-basic-multiple" multiple id="options">
                <option value="volvo">Volvo</option>
                <option value="saab">Saab</option>
                <option value="fiat">Fiat</option>
                <option value="audi">Audi</option>
        </select>
</div>

```
# JavaScript
Include the following script in your Blade template to handle the change event of the multiselect input. This script will update the Livewire component's property **selectedOptions** with the selected values.

```js
@script
  <script>
  
       $(document).ready(function() {
          $('#options').on('change', function(e){
              // let selectedValues =  e.target.value;
              let selectedValues =  $(this).val();
              $wire.$set('selectedOptions', selectedValues);
          });
      });
  
  </script>
@endscript
```

## component 
### Livewire Component (app/Http/Livewire/YourComponent.php)
In your Livewire component class, declare the **selectedOptions** property.
```php
namespace App\Http\Livewire;

use Livewire\Component;
use App\Models\Attribute;

class YourComponent extends Component
{
    public $selectedOptions = [];

    public function render()
    {
        return view('livewire.your-component');
    }
}
```

## Note
Make sure you have jQuery and the select2 library included in your project.

```
<!-- Include select2 CSS -->
<link href="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/css/select2.min.css" rel="stylesheet" />
```
```
<!-- Include jQuery -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- Include select2 JS -->
<script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js"></script>

<!-- Initialize select2 -->
<script>
    $(document).ready(function() {
        $('.js-example-basic-multiple').select2();
    });
</script>

```





