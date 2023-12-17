# Can you provide an example of when you would use an Entity over a Value Object?

### Short Answer
You would use an Entity over a Value Object when you need to track and maintain the identity of an object through its lifecycle, despite changes in its attributes. A common example is a user account in a system, which remains distinct and identifiable regardless of changes in its attributes like name, email, or password.

### Detailed Answer
1. **Example Scenario - User Account in a System**:
    - **Requirement for Identity**: In a system where users can register and manage accounts, each user account needs to be uniquely identifiable. This is crucial for tracking user activities, permissions, and preferences over time.
    - **Changing Attributes**: User attributes such as name, email, or password may change, but the account itself – the entity – remains the same.

2. **Implementation as an Entity**:
    - **Unique Identifier**: Each user account is assigned a unique identifier (like a user ID).
    - **Mutable Attributes**: The account can have mutable attributes, such as profile information, that can be updated without altering the account's identity.
    - **Lifecycle Management**: The account has a lifecycle (created, possibly suspended, or deleted) that needs to be tracked and managed.

3. **Contrast with a Value Object**:
    - **Value Object Usage**: In the same system, you might use Value Objects for elements that don't require a distinct identity, such as an address or a set of preferences. These are defined by their attributes and are replaceable when those attributes change.
    - **Immutability**: If a user decides to change their address, the system would replace the old address value object with a new one, as value objects are immutable.

### Importance in Work
Choosing between an Entity and a Value Object is a fundamental decision in Domain-Driven Design that affects how you model and implement your domain. Entities are critical for representing objects that have a distinct identity and continuity throughout the application, while Value Objects simplify and clarify the model where identity is not needed.

### Diagram/Table
Entity vs. Value Object in User Account System:

| Object Type | User Account (Entity)                       | Address (Value Object)                  |
|-------------|---------------------------------------------|-----------------------------------------|
| Identity    | Identified by user ID                       | No unique identity; defined by attributes |
| Attributes  | Name, email, password (mutable)             | Street, city, zip code (immutable)      |
| Lifecycle   | Created, updated, deleted                   | Replaced if any attribute changes       |