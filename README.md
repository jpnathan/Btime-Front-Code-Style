# Project brief
- Developed with Angular (Version 5) and its technologies such as Webpack, Karma, Jasmine and Protractor

# Plugins
- All IDEs/editors must have [editorConfig](https://editorconfig.org/) and [tslint](https://palantir.github.io/tslint/) installed/configured.
    - Editor config example [here](https://gist.github.com/jpnathan/c132b00d88e12272865ba6b92e302b18).
    - TsLint config [here](https://gist.github.com/281a458e592356892d5d1c325b321d9c).

# Dependencies
- @angular/cli: "^1.7"
- node: "8.9.4"

# Setup
```bash
npm i @angular/cli@1.7 node@8.9.4
npm install
```

# Init
- Local environment
    - `npm start`
- Development environment
    - `npm start-dev`
- Staging environment
    - `npm start-staging`
- Production environment
    - `npm start-prod`

# Folders and Files
```bash
├── ...
├── src
|  ├── app
|  |   ├──  base
|  |   ├──  contracts               # All interfaces of the project
|  |   ├──  forms                   # Reactive forms declaration
|  |   ├──  guards
|  |   ├──  interceptors
|  |   ├──  models                  # Models for requests and responses
|  |   ├──  pages                   # Declaration of pages
|  |   ├──  services
|  |   ├──  ├── ...
|  |   ├──  ├── http                # Services for HTTP requests
|  |   ├──  shared                  # Shared components, directives and pipes
|  |   |    ├── components
|  |   |    ├── directives
|  |   |    ├── pipes
├── assets                          # Assets such as images, icons, translate and etc.
├── environments                    # Environments declaration
├── scss                            # Global styles
└── ...
```

# Recommendations
- In any file all lines should respect max 80 chars.
- If necessary, create a `index.ts` file to `export` more than one `declarations`.
    - Example:
        ```typescript
        export * from './ICheckListForm';
        export * from './ICheckListFormControl';
        export * from './check-list.form';
        ```

# Interface declaration
- Interface name **must** begins with `I` letter and **must** use **PascalCase**.
- Example:
    ```typescript
    export interface IInterfaceExample {
      key: 'value',
      key1: 'value1',
      key2: 'value2'
    }
    ```

# Within a Class declaration
#### `Declaration Order`
- import
- Properties
- Constructor
- Static Methods
- Angular Hooks
- Others Methods

#### `imports`
- Declare Angular Core imports in first line and give a break line after others.
- Example:
  ```typescript
  import { Component, OnInit } from '@angular/core';

  import { CUSTOMER_OPTIONS } from '@app/pages/customers/list/list.options';
  import { IListComponent } from '@app/contracts';
  ```

#### `Configuration Properties/Variables`
- Configuration properties **must** be declared with `UpperCase`.
- Example:
  ```typescript
  export const CUSTOMER_OPTIONS: Array<IOptionItem> = [
    {
      name: 'customer.title',
      path: '/customers',
      moduleOption: 'customer'
    },
    {
      name: 'customer.group',
      path: '/customers/groups',
      moduleOption: 'group'
    }
  ]
	```

#### `Properties`
- All properties **must** have `type` and `visibility` declaration.
- **Static** properties **must** be declared with `UpperCase`.
- Example:
  ```typescript
  private static readonly MODULE_NAME = 'customer';
  protected readonly ENTITY_NAME = ListComponent.MODULE_NAME;

  public optionsItens: Array<IOptionItem> = CUSTOMER_OPTIONS;
  public selected: Array<IListCustomerComponent>;
  public columns: Array<IColumn> = COLUMNS;
  public customerRules: IModuleRoleConfigurationResponse;
  ```

#### `Methods`
- Class methods **must** be declared with `camelCase` and have return `type`.
- Parameters **must** have `type` declaration
- Example:
  ```typescript
  public changeColumns(columns: Array<IColumn>): Promise<any> {
    this.datatables.setActiveColumns();
  }
  ```

#### `Methods with Promise`
- Class methods **must** be declared with `camelCase` and have return `type`.
- Parameters **must** have `type` declaration
- Example:
  ```typescript
  public changeColumns(columns: Array<IColumn>): Promise<any> {
    return new Promise(resolve => {
      this.datatables.setActiveColumns();
      return resolve();
    })
  }
  ```

# Tests
- Use the default file name provided by `Angular Cli`

# Pull Requests
#### Recommendation

- Internal projects should name branches and pull requests with same ID as the Jira tasks.
- Example:
	- Jira task: B2-420
	- Branch: B2-420
	- Pull Request: B2 420
- Each pull request and branch created should have the ID of a main task and not sub-tasks.
- Always use Jira time-trackers on sub-tasks.
- Each pull request should contain business rules (the task itself), unit/behavior tests and WebAPI endpoints.

#### Requirements

- All Pull Requests created must be followed with one of the labels below:
	- ready to merge
	- not ready (DO NOT MERGE)
- When not ready tag should be used?
- When a service uses another service and that service isn't ready (a description must be provided in that case)
- When a service uses some package and the package isn't ready (a description must be provided in that case)
- When frontend uses some backend PR (a description must be provided in that case)
- When code review was made and changes were requested
