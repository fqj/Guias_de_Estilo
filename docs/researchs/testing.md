## Why Bother with Test Discipline?

Your tests are your first and best line of defense against software defects. Your tests are more important
than linting & static analysis (which can only find a subclass of errors, not problems with your actual 
program logic). 

**Tests are as important as the implementation itself (all that matters is that the code 
meets the requirement — how it’s implemented doesn’t matter at all unless it’s implemented poorly)**.

## Things that testing can do for you
 
 * **Design aid**: Writing tests first gives you a clearer perspective on the ideal API design.
 * **Feature documentation** (for developers): Test descriptions enshrine in code every implemented 
   feature requirement.
 * **Test your developer understanding**: Does the developer understand the problem enough to articulate 
   in code all critical component requirements?
 * **Quality Assurance**: Manual QA is error prone. In my experience, it’s impossible for a developer to remember 
   all features that need testing after making a change to refactor, add new features, or remove features.
 * **Continuous Delivery Aid**: Automated QA affords the opportunity to automatically prevent broken builds from being
   deployed to production.

##The different types of test

The first thing you need to understand about different types of tests is that they all have a job to do. They play important 
roles in continuous delivery.

You should isolate unit tests, integration tests, and functional tests from each other so that you can easily 
run them separately during different phases of development.

* **Unit tests** ensure that individual components of the app work as expected. Assertions test the component API.
* **Integration tests** ensure that component collaborations work as expected. Assertions may test component API,
    UI, or side-effects (such as database I/O, logging, etc…)
* **Functional tests** ensure that the app works as expected from the user’s perspective. Assertions primarily 
    test the user interface.


## What are Unit tests?

Unit tests exist to test individual units of software functionality. A unit is a module, component, or function. 
They’re bits of the program that can work independently of the rest of the program. The presence of unit testing 
implies that the software is designed in a modular fashion. You may hear once in a while that there are ways to make 
software “more testable.”

If you find that it’s hard to write unit tests for your program without mocking lots of other things, that’s a sign
that your program is not modular enough. Revealing tight coupling (the opposite of modularity) is one of the many 
important roles that unit tests play in software creation.

> The more you break your problems down into simple, pure functions, the easier it will be to test your code without mocks.

Unit tests should be:

* Dead simple.
* Lightning fast.
* A good bug report.
   
### The Unit Test as a Bug Report

When a test fails, that test failure report is often your first and best clue about exactly what went wrong — the
secret to tracking down a root cause quickly is knowing where to start looking. That process is made much easier when 
you have a really clear bug report.

What’s in a good test failure bug report?

1. Which component is under test?
2. What is the expected output (expected behavior)?
3. What was the actual output (actual behavior)?
4. How is the behavior reproduced?

The first three questions should be visible in the failure report. The last question should be clear from
the test’s implementation.

> When a unit tests fails, the error message is your bug report.


## Integration Tests

Integration tests ensure that various units work together correctly. For example, a Node route handler might take
a logger as a dependency. An integration test might hit that route and test that the connection was properly logged.

Many integration tests test interactions with services, such as 3rd party APIs, and may need to hit the network in 
order to work. For this reason, integration tests should always be kept separate from unit tests, in order to keep
the unit tests running as quickly as they can.

## Functional Tests

Functional tests are automated tests which **ensure that your application does what it’s supposed to do from the 
point of view of the user**. Functional tests feed input to the user interface, and make assertions about the output
that ensure that the software responds the way it should.

Functional tests are sometimes called end-to-end tests because they test the entire application, and it’s hardware
and networking infrastructure, from the front end UI to the back end database systems. In that sense, functional 
tests are also a form of integration testing, ensuring that machines and component collaborations are working as
expected.

Functional tests typically have thorough tests for “happy paths” — ensuring the critical app capabilities, 
such as user logins, signups, purchase work flows, and all the critical user workflows all behave as expected.

Functional tests should be able to run in the cloud on services such as Sauce Labs, which typically use the 
WebDriver API via projects like Selenium.

They work by simulating actions the end user might take in order to accomplish their goals in your app. They can
click buttons, input text, wait for things to happen on the page, and make assertions by looking at the actual 
UI output.

#### Smoke Tests
After you deploy a new release to production, it’s important to find out right away whether or not it’s working as 
expected in the production environment. You don’t want your users to find the bugs before you do — it could chase
them away!

It’s important to maintain a suite of automated functional tests that act like smoke tests for your newly deployed 
releases. Test all the critical functionality in your app: The stuff that most users will encounter in a typical 
session.

Smoke tests are not the only use for functional tests, but in my opinion, they’re the most valuable.


## Unit Testing in Angular 2


### Testing a component

First of all we need to import all the tools we will use:

```
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { By }              from '@angular/platform-browser';
import { DebugElement }    from '@angular/core';
```

then the component to be tested itself:

```
import { StnSideMenuComponent } from "./components/sample.component";
```

The `TestBed` is the first and most important of the Angular testing utilities. It creates an Angular testing module — an @NgModule class — that you
configure with the configureTestingModule method to produce the module environment for the class you want to test. 

Call configureTestingModule within a BeforeEach so that, before each spec runs, the TestBed can reset itself to a base state. The base state 
includes a default testing module configuration consisting of the declarables (components, directives, and pipes) and providers (some of them mocked) 
that almost everyone needs.

Lets proceed with the test:

```
describe('component test suite', () => {

  let comp:    MySampleComponent;
  let fixture: ComponentFixture<MySampleComponent>;
  let de:      DebugElement;
  let el:      HTMLElement;

  // provide our implementations or mock-data to the dependency injector
  beforeEach(() => {

    TestBed.configureTestingModule({
      declarations: [StnSideMenuComponent], // declare the test component
    });

    fixture = TestBed.createComponent(StnSideMenuComponent);
    comp = fixture.componentInstance;

    // query for the title <h1> by CSS element selector
    de = fixture.debugElement.query(By.css('h1'));
    // Or queryAll
    el = de.nativeElement;
    
  }); 
  
});  
```
    
  The createComponent` method returns a ComponentFixture, a handle on the test environment surrounding the created component. 
  The fixture provides access to the component instance itself and to the DebugElement which is a handle on the component's 
  DOM element. **It also closes the current TestBed instance to further configuration**.
  ``
   > Do not re-configure the TestBed after calling createComponent.
  
  The query method takes a predicate function and searches the fixture's entire DOM tree for the first element that satisfies 
  the predicate. The result is a different DebugElement, one associated with the matching DOM element
  
  The `By` class is a class for producing predicates, a predicate A predicate is a function that returns a boolean. A query predicate 
  receives a DebugElement and returns true if the element meets the selection criteria.
 
  Finally, the setup assigns the DOM element from the DebugElement nativeElement property to el. The tests will assert 
  that el contains the expected title text:
  
```
  it('should display original title', () => {
    fixture.detectChanges();
    expect(el.textContent).toContain(comp.title);
  });
  
  it('should display a different test title', () => {
    comp.title = 'Test Title';
    fixture.detectChanges();
    expect(el.textContent).toContain('Test Title');
  });
  
```

These tests ask the DebugElement for the native HTML element to satisfy their expectations. The full tests finally looks like this:

```
describe('component test suite', () => {

  let comp:    MySampleComponent;
  let fixture: ComponentFixture<MySampleComponent>;
  let de:      DebugElement;
  let el:      HTMLElement;

  // provide our implementations or mock-data to the dependency injector
  beforeEach(() => {

    TestBed.configureTestingModule({
      declarations: [StnSideMenuComponent], // declare the test component
    });

    fixture = TestBed.createComponent(StnSideMenuComponent);
    comp = fixture.componentInstance;

    // query for the title <h1> by CSS element selector
    de = fixture.debugElement.query(By.css('h1'));
    // Or queryAll
    el = de.nativeElement;
    
  }); 
  
  it('should display original title', () => {
     fixture.detectChanges();
     expect(el.textContent).toContain(comp.title);
  });
    
  it('should display a different test title', () => {
     comp.title = 'Test Title';
     fixture.detectChanges();
     expect(el.textContent).toContain('Test Title');
  });
  
});  
```

> The TestBed.createComponent() does not trigger change detection.
 
In production environment angular detects changes automatically, in testing environment we have to explicitly call ```detectChanges()``` 
to tell angular that something has changed so it should trigger the change detection process.
   
There are some cases where a component has an external template specified by its parameter `templateUrl`. Those cases are a problem 
for testing because the framework has to fetch external files which by nature involves asynchronous methods. The previous test won`t work under that
circumstances.
   
So what can we do?? Well, there exist the `async` function for that purpose, lets proceed first importing it:
 
```
import { async } from '@angular/core/testing';
```
 
The test setup for MySampleComponent must give the Angular template compiler time to read the files. Starting from were we left off,
the logic would be to split the setup into two beforeEach calls. The first beforeEach handles asynchronous compilation, and the second one
proceeds as usual:

 ```
  // async beforeEach
  beforeEach(async(() => {

    TestBed.configureTestingModule({
      declarations: [ MySampleComponent ], // declare the test component
    })
    .compileComponents();  // compile template and css
    
  }));
  
  // synchronous beforeEach
  beforeEach(() => {
    fixture = TestBed.createComponent(MySampleComponent);
  
    comp = fixture.componentInstance; // MySampleComponent test instance
  
    // query for the title <h1> by CSS element selector
    de = fixture.debugElement.query(By.css('h1'));
    el = de.nativeElement;
  });
  
 ```
 
And YES, we could only use `async().then() ` on the first one but for readability reasons it is recommended to
split it between two forEach(s). Don't worry, the second one will get executed only after the first (the async one) has finished. 

As we said before the `TestBed.configureTestingModule` method returns the TestBed class so you can chain calls to other TestBed 
static methods such as the above `compileComponents()`. 

> The compileComponents() method asynchronously compiles all the components configured in the testing module.

> Calling compileComponents closes the current TestBed instance for further configuration. 
Make compileComponents the last step before calling TestBed.createComponent to instantiate the component-under-test.

When `compileComponents` completes, the external templates and css files have been "inlined" and `TestBed.createComponent` can create 
new instances of MySampleComponent synchronously.


### Test a component with a dependency

Components often have service dependencies. Let suppose that our MySampleComponent depends on a external UserService for retrieving
user information and the method worth testing, so in our TestBed: 

```
TestBed.configureTestingModule({
   declarations: [ MySampleComponent ],
// providers:    [ UserService ]  // NO! Don't provide the real service!
                                  // Provide a test-double instead
   providers:    [ {provide: UserService, useValue: userServiceStub } ]
});
```

A component-under-test doesn't have to be injected with real services. In fact, it is usually better if they are 
test doubles (stubs, fakes, spies, or mocks). The purpose of the spec is to test the component, not the service, and real services
can be trouble. 

Declaring our provider we tell the TestBed to use our stub instead of the real UserService wherever it gets called.

```
userServiceStub = {
  isLoggedIn: true,
  user: { name: 'Test User'}
};
```

Angular has a hierarchical injection system, so you have an injector on every level. If you want to get a reference of what is actually
injected into the component you can get it from the injector of the component under test:

```
// UserService actually injected into the component
userService = fixture.debugElement.injector.get(UserService);
```

> The component injector is a property of the fixture's DebugElement.

Or directly from the module root injector:

```
// UserService from the root injector
userService = TestBed.get(UserService);
```

**Important:** The userService instance injected into the component is a completely different object than the declared on the test
, instead it's a clone of the provided userServiceStub. So changing the source stub once injected does not affect the service behaviour
or state on the component.

```javascript
 beforeEach(() => {
 
    // stub UserService for test purposes
    userServiceStub = {
      isLoggedIn: true,
      user: { name: 'Test User'}
    };

    TestBed.configureTestingModule({
       declarations: [ MySampleComponent ],
       providers:    [ {provide: UserService, useValue: userServiceStub } ]
    });

    fixture = TestBed.createComponent(MySampleComponent);
    comp    = fixture.componentInstance;

    // UserService from the root injector
    userService = TestBed.get(UserService);

    //  get the "welcome" element by CSS selector (e.g., by class name)
    de = fixture.debugElement.query(By.css('.welcome'));
    el = de.nativeElement;
    
 });
 
 it('should welcome the user', () => {
 
   fixture.detectChanges();
   const content = el.textContent;
   expect(content).toContain('Welcome', '"Welcome ..."');
   expect(content).toContain('Test User', 'expected name');
   
 });
 
 it('should welcome "Bubba"', () => {
 
   userService.user.name = 'Bubba'; // welcome message hasn't been shown yet
   fixture.detectChanges();
   expect(el.textContent).toContain('Bubba');
   
 });
```

### The inject function

The inject function is one of the Angular testing utilities. It injects services into the test function where you can 
alter, spy on, and manipulate them. It is the equivalent of the previous `TestBed.get(UserService)` but at function level.

It uses the current TestBed injector and can only return services provided at that level. It does not return services from component
providers.

The inject function has two parameters:

1. An array of Angular dependency injection tokens
2. A test function whose parameters correspond exactly to each item in the injection token array

ex:

```typescript
    it('should evaluate a service', inject([Router], (router: Router) => { 
    
      const spy = spyOn(router, 'navigateByUrl');
    
      heroClick(); // trigger click on first inner <div class="hero">
    
      // args passed to router.navigateByUrl()
      const navArgs = spy.calls.first().args[0];
    
      // expecting to navigate to id of the component's first hero
      const id = comp.heroes[0].id;
      expect(navArgs).toBe('/heroes/' + id,
        'should nav to HeroDetail for first hero');
    }));
```

### Testing a component with an real asynchronous service
 
When you want to test component who expects asynchronous responses from a service you could use a Spy: 
 
```javascript
beforeEach(() => {
    TestBed.configureTestingModule({
       declarations: [ TwainComponent ],
       providers:    [ TwainService ],
    });

    fixture = TestBed.createComponent(TwainComponent);
    comp    = fixture.componentInstance;

    // TwainService actually injected into the component
    twainService = fixture.debugElement.injector.get(TwainService);

    // Setup spy on the `getQuote` method
    spy = spyOn(twainService, 'getQuote')
          .and.returnValue(Promise.resolve(testQuote));

    // Get the Twain quote element by CSS selector (e.g., by class name)
    de = fixture.debugElement.query(By.css('.twain'));
    el = de.nativeElement;
    
  });

  it('should not show quote before OnInit', () => {
    expect(el.textContent).toBe('', 'nothing displayed');
    expect(spy.calls.any()).toBe(false, 'getQuote not yet called');
  });
```  

The spy is designed such that any call to getQuote receives an immediately resolved promise with a test quote. The spy bypasses 
the actual getQuote method and therefore will not contact the server.
  
### The asynchronous it  

Even when in the previous case the service responses with a resolved promise immediately, we can merely check if the function has been
called but not for the value that has been resolved. For that scenario we need to wait for the value to become available when the 
javascript engine has done the full turn. We can use the same 'async()' function from above in the 'it' implementation:

```javascript
it('should show quote after getQuote promise (async)', async(() => {
  fixture.detectChanges();

  fixture.whenStable().then(() => { // wait for async getQuote
    fixture.detectChanges();        // update view with quote
    expect(el.textContent).toBe(testQuote);
  });
}));
``` 

This test has no direct access to the promise returned by the call to twainService.getQuote because it is buried inside 
TwainComponent.ngOnInit and therefore inaccessible to a test that probes only the component API surface.

The `ComponentFixture.whenStable()` method returns its own promise which resolves when the getQuote promise completes. In fact,
the whenStable promise resolves when all pending asynchronous activities within this test complete ... the definition of "stable".

> it also exist the 'fakeAsync()' which it's a variant of async but provides more of a linear type reading (not covered here)

Another way is to use the traditional `done()` callback of the 'it' function:

```javascript
it('should show quote after getQuote promise (done)', done => {
  fixture.detectChanges();

  // get the spy promise and wait for it to resolve
  spy.calls.mostRecent().returnValue.then(() => {
    fixture.detectChanges(); // update view with quote
    expect(el.textContent).toBe(testQuote);
    done();
  });
});
```
 
Even when the done() callback is generally discouraged it could cover cases where the async or fakeAsync implementation is not enough.

### Testing an input & output component


### End to end (e2e) testing with protractor

Testing end to end it is like testing from the user point of view. By simulating the user
behaviour we can test that an application flow right from start to finish is behaving as expected.

The purpose of performing end-to-end testing is to identify system dependencies and to ensure that the data integrity 
is maintained between various system components. Given that the purpose is not testing isolated components of the system, taking
the the user point of view we can integrally test things working together like database access, network, communicating with 
the other systems and application etc.

So, in first place we need a tool capable o behaving like a user but from a programmable perspective, and that is Selenium Webdriver.
Selenium let us automate the browser.

Angular specifically uses Protractor. Protractor sits on top of Selenium, is a framework dedicated to end-to-end testing 
AngularJS applications. It allows running tests against a wide range of browsers. Since it is tailor-made for AngularJS, it 
can seep into the application life cycle. And so it knows when a particular asynchronous operation has ended, thus liberating 
you from the need to explicitly force the browser to sleep or wait for a given event.

Sample test:

```
describe("sample test suite", () => {
  it("should display proper welcome message", () => {
    browser.get("http://my-site.com")
 
    const welcomeMessageLocator = by.id("welcome-message");
    const welcomeMessageElementFinder = element(welcomeMessageLocator);
 
    expect(welcomeMessageElementFinder.getText()).toBe("Welcome Angular 2 Developer!");
  });
});
``