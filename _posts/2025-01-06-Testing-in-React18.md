---
  title: Testing in React 18
  category: Blog
  tags: 
    - react
    - testing
---

# Testing in React

## Type of Test
- test redering
- test interaction

## Creating Testable Components
- extract pure component: only depends on Props; no states and no effects
  - test rendering
- container component: manage states and business logic
  - test interaction
 
## Test Component Rendering
- render the component
- finding element
- debugging:
  - `screen.debug(screen.getByPlaceholderText('Filter'));`
  - `logRoles(element);`
  - `screen.logTesingPlaygroundURL();`
- test asynchronous rendering:
  - `await screen.findByText('... or not to be');`
  - generally:
    ```javascript
    await waitFor( () => {
      screen.getByText('... or not to be');
    });
    ```
- jest-dom:
  ```javascript
  render(<p ClassName='Selected' />);

  expect(listitem).toHaveClass('selected');
  ```
  if use jest to check the result, it would be
  ```javascript
  render(<p ClassName='Selected' />);

  expect(listitem.className).toMatch(/selected/);
  ```

  ## Test Component Interaction
  - user-event API
 
  - fireEvent API
 
  ## Test Component That Include useEffect
  - mock the api call
    ```javacript
    jest.mock('../api');
    api.getPlanets.mockResolvedValue(listOfExoplanets);
    ```
    
  - useEffect is async, need to wait for the call complete 
    ```javascript
    await within(list).findAllByRole('listitem'); // findAllByRole is async and wait up to 1 second
    ```
