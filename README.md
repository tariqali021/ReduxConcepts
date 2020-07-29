
# Redux

**Why**
- We can not set global variables to manage states. The reason is tha React does not reacts well with global variables.
    
**What**
- This is like a central place where you manage the entire state. 
- This manages & updates states of components globally. 
- Three buliding blocks are Actions (Dispatched by components), Reducers, Subscriptions.

**How** (This does not update store directly.)
    
- Create default state
    eg: 
        const initialState = { counter : 0 }

- Create a Reducer
    eg : 
        const rootReducer = (state = initialState, action) => {
            if(action.type == 'INC_COUNTER'){
                ...state, 
                counter : state.counter + action.value
            }
            return state;
        }

- Create a Store
    eg :
        const store = redux.createStore(rootReducer);   // store.getState();

- Dispatch Actions
    eg :
        store.dispatch( { type : 'INC_COUNTER' , value='10' })

- Trigger subscription
    eg :
        store.subscribe( () => {
            console.log(store.getState()); // whenever the stae is update, mean action is dispatched then subscribe method is automatically called.
        });

### Actions
    
    - basically the events triggered in component like add, remove, delete etc..
### Reducers
    - A pure function that receives state & action as input and return only the state.
### Subscription
    - Store triggers all subscriptions whenever the state is updated, and passed this state back to component as props.

### Store
    - Store is initialized with reducer. We have only one reducer either single or combined by multiple.


### Where to use 
    
- Local UI State        [ Mostly handled within components ]
    eg: 
        - update style, show/hide modal etc..
- Persistent State      [ Use Redux for relevant slices but not for whole state ]
    eg:
        - actions related to Database like all users/posts etc..
- Client State          [ Mangaed via Redux ]
    eg:
        - actions related to session handling like isUserAuthenticated, filterSetByUser etc...

### Where not to use
    
- For two way binding


# Middleware 
    
- Function or coder you hook into process that then executed as a part process without stoping it.
- Normally runs between 'after action dispatched' & 'before reaching to reducer'
- used to filter, log or anything with the dispatched action before reachingto reducer.
- This takes store as input that takes next (a function) as input that takes action (a dispatched action) as input and logs that action
- To hook any middleware to store, pass it to applyMiddleware function as an input. The applyMiddleware function can be passed to createStore as 2nd argument.
    
    eg: // custom Middleware
        
    const logger = store => {
        return next => {
            return action => {
                console.log(store.getState());
                return next(action);
            }
        }
    }

    const store = createStore(reducer, applyMiddleware(logger));
