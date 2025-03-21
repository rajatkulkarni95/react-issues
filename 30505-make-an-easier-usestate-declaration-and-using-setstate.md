# Make an easier useState declaration and using setState

> Issue #30505 - Created on 7/30/2024

> Original URL: https://github.com/facebook/react/issues/30505

## Description

Make a setValue function a method within state itself.
Right now we declare state like
const [value, setValue] = useState('')
It is already a time to make that easier. Isn't there a way to make some syntax like
const value = useStateWithSetMethod('')
value.set('this is it');// or .setValue or .setState
Really, it is only matter of making a method instead of setFunction everytime with every state with different name. There is no need to give them a different name if it is setValue or setState method within state, cause you call it from a state which already has unique name.
You even don't have to add a new whole hook. Just make a wrapper around useState and call it new name like useStater. And that wont break anything cause there's no hook change or add. 
Something like
function useStater(ininitialValue) {
const [value, setValue] = useState(initialValue);
value.setValue = setValue; //or .setState for better readibility
return value;
}
I can do it in my own lib and doing right now, but it is easier and better DX to make it by default. Especially compared to vue which already has something like this by default
