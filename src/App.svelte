<script>
	import { createEventDispatcher } from 'svelte';
	import Select from 'svelte-select';
  
	const dispatch = createEventDispatcher();
  
	let options = [
	  { label: 'Option 1', value: 'option1' },
	  { label: 'Option 2', value: 'option2' },
	  { label: 'Option 3', value: 'option3' },
	  { label: 'Option 4', value: 'option4' },
	  { label: 'Option 5', value: 'option5' },
	  { label: 'Option 6', value: 'option6' },
	  { label: 'Option 7', value: 'option7' },
	  { label: 'Option 8', value: 'option8' },
	  { label: 'Option 9', value: 'option9' },
	];
  
	const groupedOptions = [
	  {
		label: 'Group 1',
		options: [
		  { label: 'Option 1', value: 'option1' },
		  { label: 'Option 2', value: 'option2' },
		  { label: 'Option 3', value: 'option3' },
		],
	  },
	  {
		label: 'Group 2',
		options: [
		  { label: 'Option 4', value: 'option4' },
		  { label: 'Option 5', value: 'option5' },
		  { label: 'Option 6', value: 'option6' },
		],
	  },
	  {
		label: 'Group 3',
		options: [
		  { label: 'Option 7', value: 'option7' },
		  { label: 'Option 8', value: 'option8' },
		  { label: 'Option 9', value: 'option9' },
		],
	  },
	];
  
	let selected = [];
  
	function handleSelection(selection) {
	  selected = selection;
	  dispatch('change', { detail: selected });
	}
  </script>
  
  <div>
	<Select
	  options={options}
	  labelField="label"
	  valueField="value"
	  groupField="group"
	  groupOptionsBy="label"
	  multiple
	  searchable
	  placeholder="Select options"
	  selected={selected}
	  onChange={handleSelection}
	/>
  </div>

  <div>
	<Select
	  options={groupedOptions}
	  labelField="label"
	  valueField="value"
	  groupField="group"
	  groupOptionsBy="options"
	  multiple
	  searchable
	  placeholder="Select options"
	  selected={selected}
	  onChange={handleSelection}
	/>
  </div>

  