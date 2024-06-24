-- LOOKING FOR COLLABORATORS 
## SMARTLIST - TYPESCRIPT PROJECT
## Description

This project is a simple drag-n-drop project using TypeScript. Users can drag-n-drop projects between different sections of the page.

## Instructions

Before we start coding, let's understand what we already have in the project.

1. `Template` tag inside of `index.html`: It's a form of boilerplate that can be re-used in the code. Since is a template, the tag is not visible in the browser till you use it.

   We have 3 different templates in the `index.html` file:

   - `project-input`: this template will be used to create a new project.
   - `single-project`: this template will be used to display a single project.
   - `project-list`: this template will be used to display a list of projects.

2. The folder structure: The `src` folder is where TypeScript files should be created, and the `dist` folder is where the compiled JavaScript files will be stored.

   - Remember: Use the JavaScript file in the `index.html`.

3. TypeScript configuration: The `tsconfig.json` file is already configured for this project. You don't need to change anything in this file. However, it is recommended you to read what properties are active in this file.

# **General Instructions**

### Common to all the steps:

- Create a branch for each step.
- Use the pattern `step<number>` for the name of the branches.
- Switch to this branch, make all changes and add them to the staging area.
- Commit with the message `Step <number> done`.
- Push the changes to the branch.
- Open a Pull Request and merge with the `main`.
- Switch back to the `main` branch.

E.g.:

- Step 1: Create a branch called `step1`.
- Finish the instructions.
- Add the file(s)/folder(s) to the stage area: `git add <options>`
- Commit with the message: `git commit -m "Step 1 done"`
- Push to the branch: `git push origin step1`
- Create a pull request to merge your `step1` branch into the `main` branch.
- Switch back to the `main` branch.
- Merge the branch into main.

  - This process will help you to finish the project and return to previous steps easily if necessary, and make the project organized.

### Compiling: Make sure that you compile the TypeScript files before running the project. You can keep the TypeScript files compiling automatically by using the `--watch` flag in the terminal.

### <ins>**Step 1:**</ins>

> Objective: Creation of Project Input Class.
>
> Expected result: Form visible in the browser.

1.1. Create a new folder called `components` and inside that, a file called `ProjectInput.ts`.

1.2. In this file, create a new class called `ProjectInput` with 2 properties:

First property: `templateElement`</br>
Second property: `hostElement`

1.3 Store the values of the `templateElement` and `hostElement` in the constructor, by getting elements by their id from the DOM.

> Remember that getting elements by their id can return `null` if the element is not found. Also, you will need type casting to tell TypeScript which element type you are getting.

> Still in the constructor, add this code below:

```typescript
// Get the content of the template
const importedNode = document.importNode(this.templateElement.content, true);
// Get the form element from the template
this.element = importedNode.firstElementChild as HTMLFormElement;
// Add a new id to the form
this.element.id = "user-input";
// Attach the form to the host element
this.attach();
```

1.4. At this point, you will probably see an error in the `this.element` line and in the `this.attach()`. This is because we haven't created the `element` property and the `attach` method yet.

1.5. Create the `element` property and the `attach` method as `private` method.

1.6. The `attach` method should append the `this.element` to the `this.hostElement`.

1.7. Now, export the `ProjectInput` class and import it in the `app.ts` file.

1.8. In the `app.ts` file, create a new instance of the `ProjectInput` class.

1.9. If you run the project with live server, you will see that the form is now visible in the browser.

1.10. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 2:**</ins>

> Objective: Add functionality to the form.
>
> Expected result: Print the form inputs on console.

2.1. In the `ProjectInput` class, add 3 new properties:

`titleInputElement`
`descriptionInputElement`
`peopleInputElement`.

2.2. In the constructor, before calling the `attach` method, get the elements by their id and store them in the new properties.

2.3. After that, call the `configure` method.

2.4. Create the `configure` method as `private` method. This method will add an event listener to the form. It will listen to the `submit` event and call the `submitHandler` method.

2.5. Create the `submitHandler` method as `private` method. This method will prevent the default behavior of the form and log the values of the form inputs.

Obs.: When using `this` inside callback methods, you will need to bind the `this` to the class.

- **Bonus:** It is time to practice `decorators`! Try to implement the `autobind` decorator in the `submitHandler` method.

> In case of using decorators, activate the `experimentalDecorators` property in the `tsconfig.json` file.

2.6. Test it in the browser. If you type something in the form and click on the submit button, you will see the values of the form inputs in the console.

2.7. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 3:**</ins>

> Objective: Add validation to the form.
>
> Expected result: Print the form inputs on console with validation.

3.1. In the `ProjectInput` class, create the `gatherUserInput` method as `private` method. This method will get the values of the form inputs and validate them. The return type of this method should be `Tuple`.

3.2. In the case of invalid data, the method should return `void` and show an alert message.

3.3. Inside of the `submitHandler` method, call the `gatherUserInput` method and store the result in a new variable called `userInput`.

3.4. If the `userInput` is an array, use the `destructuring` to get the values of the array and log them in the console.

3.5. To finalize the form, create the `clearInputs` method as `private` method. This method will clear the values of the form inputs.

3.6. Call the `clearInputs` method inside of the `submitHandler` method, after logging the values of the form inputs.

3.7. Test it in the browser. If you type something in the form and click on the submit button, you will see the values of the form inputs in the console. Make sure that you test the invalid data as well.

3.8. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 4:**</ins>

> Objective: Making the validation reusable.
>
> Expected result: Same as the previous step, but with the code refactored.

4.1. Create a new folder called `helpers` and inside that, a file called `validation.ts`.

4.2. In the `validation.ts` file, copy and paste this interface:

```typescript
interface Validatable {
  value: string | number; // The value of the input
  required?: boolean; // If the input is required
  minLength?: number; // The minimum length of the input (for strings)
  maxLength?: number; // The maximum length of the input (for strings)
  min?: number; // The minimum value of the input (for numbers)
  max?: number; // The maximum value of the input (for numbers)
}
```

4.3. In the `validation.ts` file, create a new function called `validate` that will receive an object as argument. This object should be of type `Validatable`.

4.4. Inside of the `validate` function, create a new variable called `isValid` and set it to `true`.

4.5. Based on the properties of the object, validate the value of the input and change the value of the `isValid` variable to `false` if the validation fails.

4.6. Return the `isValid` variable.

4.7. In the `ProjectInput` class, import the `validate` function and `Validatable` interface from the `validation.ts` file.

4.8. In the `gatherUserInput` method, create new variables called `titleValidatable`, `descriptionValidatable` and `peopleValidatable`. These variables should be of type `Validatable`. Set the properties of these variables based on the properties of the form inputs.

4.9. Call the `validate` function for each of the variables inside of the if statement. If the validation fails, show an alert message.

4.10. Test it in the browser and make sure that our refactored validation is working.

4.11. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 5:**</ins>

> Objective: Render the projects
>
> Expected result: To see two lists in the browser.

5.1. Create a new file called `projectList.ts` inside the `components` folder.

5.2. In the `projectList.ts` file, create a new class called `ProjectList` with 3 properties:

`templateElement`, `hostElement` and `element`.

5.3. The constructor should receive `type` as argument. This argument should be an union type and should be either `active` or `finished`. Use shorthand syntax to initialize the property as `private`.

5.4. Inside the constructor, copy from the constructor of the `ProjectInput` class and make the necessary changes.

5.5. The `id` of the element should be `#${this.type}-projects`.

5.6. Create the `attach` method as `private` method. This method should append the `this.element` to the `this.hostElement`.

5.7. Create the `renderContent` method as `private` method.

5.8. Inside of the `renderContent` method, create a new variable called `listId` and set it to `#${this.type}-projects-list`.

5.9. Set the `id` of the `ul` element to `listId`.

5.10. Set the `textContent` of the `h2` element to `this.type.toUpperCase() + ' PROJECTS'`.

5.11. Call the `renderContent` method after the `attach` method in the constructor.

5.12. In the `app.ts` file, import the `ProjectList` class.

5.13. Create two new instances of the `ProjectList` class and pass `active` and `finished` as argument.

5.14. Test it in the browser. You should see two lists in the browser.

5.15. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 6:**</ins>

> Objective: Render the project information.
>
> Expected result: To see the projects information in the lists.

6.1. Create a new file called `ProjectState.ts` inside the `components` folder.

6.2. In the `ProjectState.ts` file, create a new class called `ProjectState` using the `singleton` pattern (check the slides about it).

6.3. This class should have `projects` as `private` property. This property should be an array of objects and should be of type `Project`, but for now, set it to `any[]` and initialize it as an empty array.

6.4. Create a new method called `addProject` that will receive `title`, `description` and `people` as arguments. This method should create a new object with these arguments, including `id` as a random number converted to `string` and push it to the `projects` array.

6.5. Create a new variable called `projectState` and set it to a instance of `ProjectState` class. Export this variable as `const`.

6.6. In the `ProjectInput` class, import the `projectState` variable from the `ProjectState.ts` file.

6.7. In the `submitHandler` method, call the `addProject` method from the `projectState` variable and pass the values of the form inputs as arguments.

6.8. In the `ProjectState` create a new `private` property called `listeners`. This property should be an array of functions and should be of type `Listener`, but for now, set it to `any[]` and initialize it as an empty array.

6.9. Create a new method called `addListener` that will receive a function `listenerFn` as argument. This method should push the `listenerFn` to the `listeners` array.

6.10. The idea is that when we add a new project, we will call all the functions inside of the `listeners` array.

6.11. After pushing the new project to the `projects` array, loop through the `listeners` array and call all the functions inside of it. Pass a copy of `projects` array as argument.

> Use the `slice` method or the spread operator to create a copy of the `projects` array.

6.12. In the `ProjectList` class, create a new property called `assignedProjects` and set it to an empty array.

6.13. Create a new method called `renderProjects`. This method should loop through the `assignedProjects` array and create a new `li` element for each project. Set the `textContent` of the `li` element to the title of the project. Append the `li` element to the `ul` element identified by `#${this.type}-projects-list`.

6.14. In the constructor of the `ProjectList` class, call the `addListener` method from the `projectState` variable and pass a function as argument. This function assign `projects` received as a parameter to the `assignedProjects` property and call the `renderProjects` method.

6.15. Test it in the browser. You should see the projects being rendered in the lists after submitting the form.

6.16. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 7:**</ins>

> Objective: Code improvement
>
> Expected result: The same as the previous step.

7.1. Create a new folder called `models` inside `src` folder and create a new file called `project.ts` inside this folder.

7.2. In the `project.ts` file, create a new class called `Project` with 4 properties: `id`, `title`, `description`, `people` and a new property that we haven't created yet called `status`.

7.3. The idea for the `status` is to filter the projects based on the status. This property should be of type `ProjectStatus` and should be an enum.

7.4. Create the `ProjectStatus` enum with 2 values: `Active` and `Finished`.

7.5. In the `ProjectState` class, change the type of the `projects` property to `Project[]`.

7.6. In the `addProject` method, instantiate a new `Project` object and pass the arguments received as parameters. Set the `status` property to `ProjectStatus.Active`.

7.7. In the `ProjectList` class, change the type of the `assignedProjects` property to `Project[]`.

7.8. In the `ProjectState` class, create a new type called `Listener` and set it to a function that receives a `Project[]` as argument and returns `void`.

7.9. In the `ProjectState` class, change the type of the `listeners` property to `Listener[]`.

7.10. In the `ProjectState` class, change the type of the `addListener` method to `addListener(listenerFn: Listener)`.

7.11. In the `ProjectList` class, when calling the `addListener` method, change the type of the parameter to `projects: Project[]`.

7.12. Test it in the browser. Everything should work as before.

7.13. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 8:**</ins>

> Objective: Fix duplicates
>
> Expected result: No projects duplications and only the possibility to add the project to the list that matches the status of the list.

8.1. In the `ProjectList` class, filter the `projects` received as parameter based on the status and assign it to the `assignedProjects` property.

8.2. That should only add the projects to the list that matches the status of the list. Test it in the browser.

8.3. If works, now we need to fix the duplication of projects in the list.

8.4. Inside of the `renderProjects` method, clear the `ul` element before looping through the `assignedProjects` array.

8.5. That is not the ideal solution, but it works for now.

8.6. Test it in the browser.

8.7. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 9:**</ins>

> Objective: Code improvement
>
> Expected result: The same as the previous step.

If you noticed, we have some duplicated code in the `ProjectInput` and `ProjectList` classes. Let's fix that.

9.1. Create a new file called `base-component.ts` inside the `components` folder.

9.2. In the `base-component.ts` file, create a new class called `Component`. This class should be abstract.

9.3. Check the common properties and these properties will be added to the `Component` class.

9.4. `templateElement`, `hostElement` and `element` are the common properties.

9.5. This class should have generic types for `hostElement` and `element`. Both should constraint to `HTMLElement`.

9.6. In the constructor, we should receive the `templateId`, `hostElementId` and `newElementId` as arguments. `newElementId` should be optional.

9.7. Copy the constructor code from the `ProjectList` class to the `Component` class. Make the necessary changes.

9.8. Copy the attach method from the `ProjectList` class to the `Component` class.

9.9. Add `configure` and `renderContent` methods to the `Component` class. Both should be abstract methods.

9.10. In the `ProjectInput` class, extends `Component` class. Make the necessary changes.

9.11. Move the `addListener` code to the `configure` method.

9.12. Do the same for the `ProjectInput` class. Make the necessary changes.

9.13.`renderContent` could be an empty method to satisfy the abstract class.

9.14. Test it in the browser. Everything should work as before.

9.15. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 10:**</ins>

> Objective: Render projects in the list.
>
> Expected result: Showing the projects in the list.

10.1. Create a new file called `ProjectItem.ts` inside the `components` folder.

10.2. In the `ProjectItem.ts` file, create a new class called `ProjectItem` and extends the `Component` class.

10.3. In the constructor, receive the `hostId` and `project` as arguments.

10.4. Inside the constructor, call the `super` method and pass the `templateId`, `hostId`, `newElementId` (id of the product) as arguments.

10.5. In the `configure` method, you can keep it empty for now.

10.6. In the `renderContent` method, set the `textContent` of the `h2` element to the `title` of the `project`.

10.7. Set the `textContent` of the `h3` element to the `people` of the `project`.

10.8. Set the `textContent` of the `p` element to the `description` of the `project`.

10.9. Instantiate the `ProjectItem` accordingly.

10.10. Test it in the browser.

10.11. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 11:**</ins>

> Objective: Specify the number of project members.
>
> Expected result: Showing the correct sentence depending on the number of members.

11.1. In the `ProjectItem` class, create a new getter method called `members` and set the return type to `string` and in this method, check if the `project.people` is equal to `1` and return `1 member assigned`.

11.2. If not, return `${this.project.people} members assigned`.

11.3. In the `renderContent` method, set the `textContent` of the `h3` element to the `members` method.

11.4. Test it in the browser.

11.5. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 12:**</ins>

> Objective: Make things draggable and droppable.
>
> Expected result: The elements will be draggable and droppable.

12.1. Inside of the `helpers` folder, create a new file called `drag-drop.ts` and in this file, create a new interface called `Draggable`, and in this interface, create a new method called `dragStartHandler` and set the return type to `void`. This method should receive an `event` with type of `DragEvent` as argument.

12.2. Same for the `dragEndHandler` method.

12.3. Create another interface called `DragTarget` and in this interface, create a new method called `dragOverHandler` and set the return type to `void`. This method should receive an `event` with type of `DragEvent` as argument.

12.4. Same for the `dropHandler` method.

12.5. Same for the `dragLeaveHandler` method. Your code should look like this:

```ts
export interface Draggable {
  dragStartHandler(event: DragEvent): void; // allow to drag
  dragEndHandler(event: DragEvent): void; // when the drag ends
}

export interface DragTarget {
  dragOverHandler(event: DragEvent): void; // when the draggable element is over the target
  dropHandler(event: DragEvent): void; // when the draggable element is dropped
  dragLeaveHandler(event: DragEvent): void; // when the draggable element is leaving the target
}
```

12.6. Implement the `Draggable` interface in the `ProjectItem` class.

12.7. Inside the `configure` method, add a event listener to the `li` element for the `dragstart` event and call the `dragStartHandler` method.

12.8. Add another event listener to the `li` element for the `dragend` event and call the `dragEndHandler` method.

Obs.: When using `this` inside callback methods, you will need to bind the `this` to the class.

- **Bonus:** It is time to practice `decorators`! Try to implement the `autobind` decorator in the `submitHandler` method.

> In case of using decorators, activate the `experimentalDecorators` property in the `tsconfig.json` file.

12.9. If you try to test it in the browser, nothing will happen. That's because we need to set the `draggable` attribute to `true` in the `li` element in the HTML file.

12.10. Add logs to console to see when the events are triggered.

12.11. Test it in the browser.

12.12. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 13:**</ins>

> Objective: Implement DragTarget interface in the ProjectList class.
>
> Expected result: The color of the target element will change to show that the droppable is working.

13.1. In the `ProjectList` class, implement the `DragTarget` interface.

13.2. Inside the `configure` method, add a event listener to the `ul` element for the `dragover` event and call the `dragOverHandler` method.

13.3. Add another event listener to the `ul` element for the `drop` event and call the `dropHandler` method.

13.4. Add another event listener to the `ul` element for the `dragleave` event and call the `dragLeaveHandler` method.

Obs.: When using `this` inside callback methods, you will need to bind the `this` to the class.

- **Bonus:** It is time to practice `decorators`! Try to implement the `autobind` decorator in the `submitHandler` method.

> In case of using decorators, activate the `experimentalDecorators` property in the `tsconfig.json` file.

13.5. In the `dragOverHandler` method, add a new class to the `ul` element called `droppable`.

13.6. In the `dragLeaveHandler` method, remove the `droppable` class from the `ul` element.

13.7. Test it in the browser. You should see the background color of the `ul` element changing when you drag the `li` element over it.

13.8. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 14:**</ins>

> Objective: Transfer data using drag an drop.
>
> Expected result: Showing in the console the data of the project.

14.1. In the `ProjectItem` class, inside of the `dragStartHandler` method, add a new property called `dataTransfer` to the `event` object and set the value to `this.project.id`. Also, set the `effectAllowed` property to `move`.

```ts
event.dataTransfer!.setData("text/plain", this.project.id);
event.dataTransfer!.effectAllowed = "move";
```

> This code will allow us to move the element and once dropped, we will be able to access the data.

14.2. In the `ProjectList` class, inside of the `dragOverHandler` method, check if the `event` object has the `dataTransfer` and include a `preventDefault` call to ensure that the drop event always fires as expected

14.3. In the `dropHandler` method, log the `event.dataTransfer!.getData('text/plain')` to see what we have access to.

14.4. Test it in the browser. You should see the `id` of the project in the console.

14.5. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 15:**</ins>

> Objective: Update the lists when the project is dropped.
>
> Expected result: You should be able to drag and drop the projects without any problem,

15.1. In the `ProjectState`, create a new method called `moveProject`. This method should receive an `id` with type of `string` as argument and `newStatus` with type of `ProjectStatus` as argument.

15.2. In the method, create a new variable called `foundProject` and set the value to the return of the `find` method on the `projects` array.

15.3. If `foundProject` is not `undefined` and the `newStatus` is different from project status, then set the `status` property to `newStatus`.

15.4. Create a new method called `updateListeners` and move the loop from `addProject` method to this method.

15.5. Call this new method in the `addProject` method and in the `moveProject` method after changing the status.

15.6. In the `ProjectList` class, inside of the `dropHandler` method, call the `moveProject` method on the `projectState` object and pass the `id` of the project and the new status of the list, depending on the type of the list.

15.7. Test it in the browser. You should see the project moving from one list to another. Try to move it back to the original list.

15.8. Save your changes following the [general instruction](#general-instructions).

### <ins>**Step 16:**</ins>

16.1 Of course, so much more improvement we can make from here. Refactor!!

16.2. Save your changes following the [general instruction](#general-instructions).

**Congratulations! You have successfully completed the project!** 🎉🎉🎉
