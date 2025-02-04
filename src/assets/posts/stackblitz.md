<strong>I love Stackblitz</strong>

Stackblitz is a awesome tool for sharing sharing live examples and prototyping. But you can do even more. With stackblitz you can kickoff a githup repo with no efford.
And you can run unit tests too.

Here I wanna show how you can run your Karma/Jasmine tests in Stackblitz.

But first things first.

### What is Stackblitz?

Stackblitz is a onlive edotor based on Visual Studio Code. You can use the same keyboard shortcuts wich are availabe in your local installation..

#### my favourite key bindings

| keys               | Function                                                                    |
| ------------------ | --------------------------------------------------------------------------- |
| alt+key-up         | Move the line where the Cursor is located one line up                       |
| alt+key-down       | Move the line where the Cursor is located one line down                     |
| alt+shift+key-up   | Copy the line where the Cursor is located one line up                       |
| alt+shift+key-down | Copy the line where the Cursor is located one line down                     |
| ctrl+d             | Set Multi Cursor. On the selected word and the next occurrence of that word |
| ctrl+#             | comment the line where the cursor is located                                |

#### Stackblitz and github

Very often you wanna show your projects to someone, or wanna test something in a project.
With stackblitz, this is a no-brainer.
Just visit

```bash
https://stackblitz.com/github/userName/repoName
```

to open your master Branch in the Browser

or

```bash
https://stackblitz.com/github/userName/repoName/tree/branch
```

to open a specific Branch

Stackblitz can run your Javascript Project, no matter if the framework.

#### set up for Karma and Jasmine

To run your Unit Tests in Stackblitz you have to do some config in the `main.ts`.

```ts
// Import Jasmine from node_modules
import jasmineRequire from 'jasmine-core/lib/jasmine-core/jasmine.js';
import 'jasmine-core/lib/jasmine-core/jasmine-html.js';
import 'jasmine-core/lib/jasmine-core/boot.js';

import './polyfills';

import 'zone.js/dist/zone-testing';

import { getTestBed } from '@angular/core/testing';
import {
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting
} from '@angular/platform-browser-dynamic/testing';

// declare it in the window object
window['jasmineRequire'] = jasmineRequire;

// setup jasmine as a global var
declare var jasmine;

// Spec files to include in the Stackblitz tests
import './tests.sb.ts';

//

bootstrap();

//

function bootstrap() {
  if (window['jasmineRef']) {
    location.reload();
    return;
  } else {
    window.onload(undefined);

    window['jasmineRef'] = jasmine.getEnv();
  }

  // First, initialize the Angular testing environment.
  getTestBed().initTestEnvironment(
    BrowserDynamicTestingModule,
    platformBrowserDynamicTesting()
  );
}
```

But for now we have no Jasmine Styling
We have to add it in the `styles.scss`

```scss
@import '~jasmine-core/lib/jasmine-core/jasmine.css';
```

Maybe you already noticed this line in the `main.ts`

```ts
// Spec files to include in the Stackblitz tests
import './tests.sb.ts';
```

In this file we have to import all the testing files `(*.spec.ts)`.

Here is an example.

```ts
import './app/app.component.spec.ts';
import './app/my-nav/my-nav.component.spec.ts';
```

That's it.
