# pyvinci
Data to GraphQL mapper 

## Usage

```python
# my_models.py

class MyModel:
    id = UUID4()
    email = Email()
    name = String()

class MyOtherModel:
    creator = UUID4()
    info = Markdown()


# my_mutations.py

async def create_smth(required_1: str, required_2: int, *, optional_1: float=None, optional_2: Any=None)->str:
    my_model = MyModel(required_1, optional_1, optional_2)
    id = await db.save(my_model)
    await db.save(MyOtherModel(id, required_2))
    return 'success'


# app.py
from my_models import MyModel, MyOtherModel
from my_mutations import create_smth

# init Schema
my_schema = pyvinci.Schema()

# register models
my_schema.register_models(MyModel, MyOtherModel)

# register mutations
my_schema.register_mutations(create_smth)

# now you can add your schema to your app
```
