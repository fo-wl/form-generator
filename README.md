# form-generator

**Schema example**

```json
{
    id: 'testInput',
    type: 'input',
    inputType: 'text',
    placeholder: 'test_i',
    label: 'Test input filed',
    disabled: true
},
{
    id: 'testSelect',
    type: 'select',
    placeholder: 'test_s',
    label: 'Test select filed',
    options: ['etsasdt', 'etst'],
    required: true
},
{
    id: 'testPassword',
    type: 'input',
    inputType: 'password',
    placeholder: 'test_p',
    label: 'Test password filed',
    options: ['etsasdt', 'etst'],
    hint: '6 simbols',
    maxlength: 6,
    required: true
},
{
    id: 'testEmail',
    type: 'input',
    inputType: 'email',
    placeholder: 'test_e',
    label: 'Test email filed'
},
{
    id: 'testCheckbox',
    type: 'input',
    inputType: 'checkbox',
    label: 'Test checkbox filed',
    required: true
}
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

