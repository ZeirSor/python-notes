# sqlalchemy框架

## 常用函数

### Relationship

**`relationship` 参数解释：**

1. `back_populates`：用于指定反向关联的属性名称，以建立双向关系。
   - 作用：指定关联的另一个类中的属性，用于建立双向关联。
   - 示例用法：在 `User` 类中，`preference` 属性的 `back_populates` 设置为 `"user"`，以建立与 `Preference` 类的反向关联。
   - 示例代码：
   
   ```python
   preference = relationship("Preference", back_populates="user", uselist=False, passive_deletes=True)
   ```

2. `uselist`：指示是否将关联的对象存储在列表中，通常用于处理一对一关系。
   
   - 作用：控制是否使用列表来存储关联对象。当设置为 `False` 时，表示一对一关系。
   - 示例用法：在一对一关系中，通常将其设置为 `False`。
   - 示例代码：
   
   ```python
   preference = relationship("Preference", back_populates="user", uselist=False, passive_deletes=True)
   ```
   
3. `passive_deletes`：启用或禁用级联删除，指示是否删除关联对象。
   - 作用：控制是否启用级联删除，如果设置为 `True`，则删除一个对象时会级联删除相关联的对象。
   - 示例用法：通常在需要级联删除的情况下设置为 `True`。
   - 示例代码：
   
   ```python
   preference = relationship("Preference", back_populates="user", uselist=False, passive_deletes=True)
   ```

4. `secondary`：定义多对多关系中的中间表。
   - 作用：指定多对多关系中的中间表，用于建立多对多关系。
   - 示例用法：在 `User` 类中，`roles` 属性的 `secondary` 设置为 `"users_roles"`，以定义多对多关系的中间表。
   - 示例代码：
   
   ```python
   roles = relationship("Role", secondary="users_roles", back_populates="users", passive_deletes=True)
   ```

总结：

-   `relationship` 中的 `back_populates` 用于建立双向关系，`uselist` 控制是否使用列表存储关联对象，`passive_deletes` 启用或禁用级联删除，`secondary` 用于定义多对多关系的中间表。

### ForeignKey

**`ForeignKey` 参数解释：**

1. `ForeignKey` 的 `ondelete`：指定外键的级联操作，定义在父表上删除一行时应采取的操作。
   
   - 作用：定义在父表上执行删除操作时，如何处理与之关联的子表的数据。
   - 示例用法：`ondelete="CASCADE"` 表示级联删除，删除父表的行时会删除相关的子表行。
   - 示例代码：
   
   ```python
   user_id = Column(Integer, ForeignKey("users.id", ondelete="CASCADE"), nullable=False, index=True, unique=True)
   ```
   
2. `nullable`：指示字段是否允许为空（`True` 或 `False`）。
   - 作用：定义字段是否可以存储空值。
   - 示例用法：通常在需要允许空值的情况下将其设置为 `True`。
   - 示例代码：
   
   ```python
   user_id = Column(Integer, ForeignKey("users.id", ondelete="CASCADE"), nullable=False, index=True, unique=True)
   ```

3. `index`：指示是否在字段上创建索引（`True` 或 `False`）。
   - 作用：定义是否为字段创建数据库索引，用于提高查询性能。
   - 示例用法：通常在需要频繁进行查询的字段上创建索引。
   - 示例代码：
   
   ```python
   user_id = Column(Integer, ForeignKey("users.id", ondelete="CASCADE"), nullable=False, index=True, unique=True)
   ```

4. `unique`：指示字段的值是否必须是唯一的（`True` 或 `False`）。
   - 作用：定义字段的值是否必须在表中是唯一的。
   - 示例用法：通常在需要保证唯一性的字段上设置为 `True`。
   - 示例代码：
   
   ```python
   user_id = Column(Integer, ForeignKey("users.id", ondelete="CASCADE"), nullable=False, index=True, unique=True)
   ```

总结：
- `ForeignKey` 中的 `ondelete` 定义了外键的级联操作，`nullable` 定义字段是否允许为空，`index` 定义是否创建索引，`unique` 定义字段值是否必须唯一。

## 代码模板

以下是一对一、一对多和多对多三种关系的伪代码模板示例：

### 一对一关系模板

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship

class Parent(Base):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    child = relationship('Child', uselist=False, back_populates='parent')

class Child(Base):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    parent_id = Column(Integer, ForeignKey('parent.id'))
    parent = relationship('Parent', back_populates='child')
```

### 一对多关系模板

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship

class Parent(Base):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    children = relationship('Child', back_populates='parent')

class Child(Base):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    parent_id = Column(Integer, ForeignKey('parent.id'))
    parent = relationship('Parent', back_populates='children')
```

### 多对多关系模板

```python
from sqlalchemy import Column, Integer, String, Table, ForeignKey
from sqlalchemy.orm import relationship

association_table = Table(
    'association',
    Base.metadata,
    Column('parent_id', Integer, ForeignKey('parent.id')),
    Column('child_id', Integer, ForeignKey('child.id'))
)

class Parent(Base):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    children = relationship('Child', secondary=association_table, back_populates='parents')

class Child(Base):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    parents = relationship('Parent', secondary=association_table, back_populates='children')
```

这些伪代码模板展示了如何使用 SQLAlchemy 来定义一对一、一对多和多对多关系。根据具体的数据模型和需求，你可以在这些模板的基础上进行修改和扩展。

## 示例代码

<p style="text-align: center;">
  <a href="https://www.youtube.com/watch?v=vKuKp10LQEM">参考视频教程</a>
</p>

### models

#### **base.py**

```python
from datetime import datetime
from sqlalchemy import Column, DateTime
from sqlalchemy.orm import declarative_base

from main import session

Model = declarative_base()
Model.query = session.query_property()

class TimeStampeModel(Model):
    __abstract__ = True

    created_at = Column(DateTime, default=datetime.now())
    updated_at = Column(DateTime, onupdate=datetime.now())
```

- **分析**：
  - 这个文件定义了一个基础的 SQLAlchemy 模型类 `TimeStampeModel`，用于包含常见的时间戳字段 `created_at` 和 `updated_at`，这些字段将用于跟踪数据库记录的创建和更新时间。
  - 这个类是一个抽象基类，意味着它不会在数据库中创建对应的表，但可以被其他模型类继承以继承时间戳字段。

#### **user.py**

```python
from sqlalchemy.orm import relationship
from sqlalchemy import Column, Integer, String, ForeignKey

from models.base import TimeStampeModel, Model

class User(TimeStampeModel):
    __tablename__ = "users"
    ...

class Preference(TimeStampeModel):
    __tablename__ = "prefrences"
    ...

class Address(TimeStampeModel):
    __tablename__ = "addresses"
    ...


class Role(Model):
    __tablename__ = "roles"
  	...

class UserRole(TimeStampeModel):
    __tablename__ = "users_roles"
	...
```

- **分析**：
  - 这个文件定义了多个 SQLAlchemy 模型类，用于建模用户、用户偏好设置、地址、角色等。
  - `User` 类定义了一对一、一对多和多对多关系。其中，`preference` 属性表示一对一关系，`addresses` 属性表示一对多关系，`roles` 属性表示多对多关系。这些关系通过 `relationship` 参数进行定义，包括 `back_populates`、`uselist`、`passive_deletes` 和 `secondary`。
  - `Preference`、`Address`、`Role`、`UserRole` 类也都继承自 `TimeStampeModel`，并定义了相应的表结构和关联关系。
  - 这些模型类用于创建数据库表以及建立它们之间的关系，实现了用户、偏好设置、地址和角色等数据的存储和关联。

##### from ... import ...

```python
from sqlalchemy.orm import relationship
from sqlalchemy import Column, Integer, String, ForeignKey

from models.base import TimeStampeModel, Model
```

- 这部分代码导入了需要使用的 SQLAlchemy 模块和基类。

##### User

```python
class User(TimeStampeModel):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, autoincrement=True)
    first_name = Column(String(80), nullable=False)
    last_name = Column(String(80), nullable=False)
    email = Column(String(80), nullable=False, unique=True)

    # one to one relationships
    preference = relationship(
        "Preference",
        back_populates="user", uselist=False, passive_deletes=True
    )
    # one to many relationships
    addresses = relationship(
        "Address",
        back_populates="user", passive_deletes=True
    )
    # many to mant relationships
    roles = relationship(
        "Role",
        secondary="users_roles", back_populates="users", passive_deletes=True
    )

    def __repr__(self):
        return f"{self.__class__.__name__}, name: {self.first_name} {self.last_name}"
```

- `User` 类表示用户模型，用于存储用户的信息。
  - `__tablename__` 指定了数据库表名为 "users"。
  - `id` 是用户的唯一标识，是主键，自增。
  - `first_name` 和 `last_name` 存储用户的名字和姓氏。
  - `email` 存储用户的电子邮件地址，且必须是唯一的。

```python
    # one to one relationships
    preference = relationship(
        "Preference",
        back_populates="user", uselist=False, passive_deletes=True
    )
```

##### Preference

```python
class Preference(TimeStampeModel):
    __tablename__ = "prefrences"

    id = Column(Integer, primary_key=True, autoincrement=True)
    language = Column(String(80), nullable=False)
    currency = Column(String(80), nullable=False)
    user_id = Column(
        Integer,
        ForeignKey("users.id", ondelete="CASCADED"),
        nullable=False, index=True, unique=True
    )

    # one to one relationship
    user = relationship("User", back_populates="preferences")

    def __repr__(self):
        return f"{self.__class__.__name__}, language: {self.language}, currency: {self.currency}"
```

- `preference` 属性定义了与 `Preference` 模型的一对一关系，表示用户与偏好设置的关联。
  - `relationship` 函数用于定义关系。
  - `"Preference"` 指定了关联的模型名称。
  - `back_populates` 参数用于指定在 `Preference` 模型中关联属性的名称，这里是 `"user"`。
  - `uselist` 参数设置为 `False`，表示一对一关系。
  - `passive_deletes` 参数设置为 `True`，表示支持被动删除。

```python
    # one to many relationships
    addresses = relationship(
        "Address",
        back_populates="user", passive_deletes=True
    )
```

##### Address

```python
class Address(TimeStampeModel):
    __tablename__ = "addresses"

    id = Column(Integer, primary_key=True, autoincrement=True)
    road_name = Column(String(80), nullable=False)
    postcode = Column(String(80), nullable=False)
    city = Column(String(80), nullable=False)
    user_id = Column(
        Integer, ForeignKey("users.id", ondelete="CASCADED"),
        nullable=False, index=True,
    )

    # one to many relationships
    user = relationship("User", back_populates="addresses", )

    def __repr__(self):
        return f"{self.__class__.__name__}, name: {self.city}"
```

- `addresses` 属性定义了与 `Address` 模型的一对多关系，表示用户与地址的关联。
  - `relationship` 函数用于定义关系。
  - `"Address"` 指定了关联的模型名称。
  - `back_populates` 参数用于指定在 `Address` 模型中关联属性的名称，这里是 `"user"`。
  - `passive_deletes` 参数设置为 `True`，表示支持被动删除。

```python
    # many to many relationships
    roles = relationship(
        "Role",
        secondary="users_roles", back_populates="users", passive_deletes=True
    )
```

##### Role

```python
class Role(Model):
    __tablename__ = "roles"

    id = Column(Integer, primary_key=True, autoincrement=True)
    name = Column(String(80), nullable=False)
    slug = Column(String(80), nullable=False, unique=True)

    # many to many relationships
    users = relationship("User", secondary="users_roles", back_populates="roles", passive_deletes=True)

    def __repr__(self):
        return f"{self.__class__.__name__}, name: {self.name}"
```

- `roles` 属性定义了与 `Role` 模型的多对多关系，表示用户与角色的关联。
  - `relationship` 函数用于定义关系。
  - `"Role"` 指定了关联的模型名称。
  - `secondary` 参数指定了中间表的名称为 `"users_roles"`。
  - `back_populates` 参数用于指定在 `Role` 模型中关联属性的名称，这里是 `"users"`。
  - `passive_deletes` 参数设置为 `True`，表示支持被动删除。

```python
    def __repr__(self):
        return f"{self.__class__.__name__}, name: {self.first_name} {self.last_name}"
```

- `__repr__` 方法定义了对象的字符串表示，用于调试和显示用户对象的信息。

总结：

- `User` 类定义了用户模型，包括用户的基本信息和与其他模型的关联关系。
- 通过 `relationship` 函数，`User` 类与 `Preference`、`Address` 和 `Role` 模型建立了一对一、一对多和多对多关系，实现了用户与偏好设置、地址和角色的关联。
- 这些关联关系在数据库中的表结构和外键关系由 SQLAlchemy 自动生成。

##### UserRole

非常抱歉之前的遗漏。以下是 `users_roles` 中间表的总结：

**文件: models/user.py**

```python
class UserRole(TimeStampeModel):
    __tablename__ = "users_roles"

    user_id = Column(Integer, ForeignKey("users.id", ondelete="CASCADE"), primary_key=True)
    role_id = Column(Integer, ForeignKey("roles.id", ondelete="CASCADE"), primary_key=True)
```

- `UserRole` 类表示 `users_roles` 中间表，用于实现多对多关系，关联用户和角色。
  - `__tablename__` 指定了数据库表名为 "users_roles"。
  - `user_id` 列是与用户表关联的外键，用于指定用户的唯一标识。
    - `Integer` 类型表示整数。
    - `ForeignKey` 函数指定了外键关联到 "users.id" 列，表示与用户表的关联。
    - `ondelete="CASCADE"` 表示在删除用户时，同时删除关联的中间表数据。
  - `role_id` 列是与角色表关联的外键，用于指定角色的唯一标识。
    - `Integer` 类型表示整数。
    - `ForeignKey` 函数指定了外键关联到 "roles.id" 列，表示与角色表的关联。
    - `ondelete="CASCADE"` 表示在删除角色时，同时删除关联的中间表数据。

- `UserRole` 类定义了 `users_roles` 中间表，用于实现多对多关系，关联用户和角色。
- 该表包括 `user_id` 和 `role_id` 两列，分别表示与用户表和角色表的关联。
- `ondelete="CASCADE"` 选项表示在删除用户或角色时，同时删除关联的中间表数据，确保数据的一致性。

