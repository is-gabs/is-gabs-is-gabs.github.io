Title: Python testings with pytest
Date: 2022-10-02 14:23
Tags: Python Tests
Category: Python

## Stack:
* Python3.6+
* Pytest


## Casos de testes:

### Métodos simples:

#### Implementação: 
```python
def helper():
    return {
	'field_1': 'value_1',
	'field_2': 'value_2'
    }
```


#### Validação de tipo:
```python
def test_should_return_a_dict():
    result = helper()

    assert isinstance(result, dict)
```

#### Validação de chaves:
```python
def test_should_return_expected_keys():
    expected_keys = {'field_1', 'field_2'}
    result = helper()
    
    assert set(result.keys()) == expected_keys
```

#### validação de valores:
```python
import pytest

@pytest.mark.parametrize(
    ('key', 'value'),
    (
        ('field_1', 'value_1'),
        ('field_2', 'value_2')
    )
)
def test_should_return_expected_values(key, value):
    result = helper()

    assert result[key] == value
```

### Métodos que chamam outros métodos:

#### Implementação:
```python
def helper():
    result = get_something()
    return result

```

#### Validação da chamada de método aninhado:
```python
from unittest import mock

@mock.patch('app.get_something')
def test_should_call_get_something_method(mocked_method):
    helper()

    mocked_method.assert_called_once()
```

#### Validação de retorno de método aninhado:
```python
from unittest import mock

@mock.patch('app.get_something')
def test_should_return_get_something_method_return(mocked_method):
    mocked_method.return_value = 'expected_value'
    result = helper()

    assert result == 'expected_value'
```

### Chamadas de métodos com parâmetros:

#### Implementação:
```python
def helper():
    do_something(param='xpto')
```

#### Validação da chamada de um método com os parâmetros esperados:
```python
from unittest import mock

@mock.patch('app.do_something')
def test_should_call_do_somethig_method_with_expected_params(mocked_method):
    helper()

    mocked_method.assert_called_once_with(param='xpto')
```