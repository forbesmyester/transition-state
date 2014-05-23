# TransitionState

A simple state machine system with the ability to control what states are valid to get to from other states.

## Example Usage

Create an instance, passing in the starting state:

	var ts = new TransitionState('ANALYZE');

Add the states, the first parameter is the is the state with a list of states which you can get to from there.

	ts.addState('ANALYZE', ['DATA_PARTIAL_OFFLINE', 'DATA_FULL_OFFLINE']);
	ts.addState('DATA_PARTIAL_OFFLINE', ['ANALYZE']);
	ts.addState('DATA_FULL_OFFLINE', ['ANALYZE']);

You can get notified when the initial state is entered:

	ts.on('initial-state',function(state) {
		console.log("Initial state " + state + " entered");
	});

Or when any other state changes occur:

	ts.on('changed-state',function(oldState, newState) {
		console.log("I am now in state " + newState + " but I was previously in " + oldState);
		console.log("Just so you know, you can also get the state at time by calling " + ts.current());
	});

When you are ready, you can start the state machine:

	ts.start();

And try and move it to other states whenever your program / app / library needs to:

	ts.change('DATA_FULL_OFFLINE');

## Source Code

Source code is prepared using [Browserify](http://browserify.org/) which is also compatible with Node.JS. There is a UMD bundle which can be used with AMD or a vanilla browser (where it will export a global called called TransitionState.
