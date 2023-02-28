<script>
  const options = [
    {
      category: 'Beef',
      foods: [
        { id: '1A', value: 'Beef and Mustard Pie' },
        { id: '2A', value: 'Beef and Oyster Pie' },
        { id: '3A', value: 'Beef Bourguignon' },
        { id: '4A', value: 'Beef Brisket Pot Roast' },
      ],
    },
    {
      category: 'Chicken',
      foods: [
        { id: '1B', value: 'Ayam Percik' },
        { id: '2B', value: 'Brown Stew Chicken' },
        { id: '3B', value: 'Chick-Fil-A Sandwich' },
        { id: '4B', value: 'Chicken & Mushroom Hotpot' },
        { id: '5B', value: 'Chicken Alfredo Primavera' },
      ],
    },
    {
      category: 'Dessert',
      foods: [
        { id: '1C', value: 'Apam Balik' },
        { id: '2C', value: 'Apple & Blackberry Crumble' },
        { id: '3C', value: 'Apple Frangipan Tart' },
        { id: '4C', value: 'Bakewell Tart' },
        { id: '5C', value: 'Banana Pancakes' },
      ],
    },
    {
      category: 'Seafood',
      foods: [
        { id: '1D', value: 'Baked Salmon with Fennel & Tomatoes' },
        { id: '2D', value: 'Cajun Spiced Fish Tacos' },
        { id: '3D', value: 'Escovitch Fish' },
        { id: '4D', value: 'Fish Fofos' },
      ],
    },
  ];

  let query = 'beefa';

  let filteredOptions = [];

  let isFocus = false;

  const handleFocus = () => {
    isFocus = true;
  };

  const handleBlur = () => (isFocus = false);

  const handleChange = (e) => {
    query = e.target.value;
    const tempFilteredOptions = options.reduce((acc, option) => {
      // check if the category matches the search input
      if (option.category.toLowerCase().includes(query.toLowerCase())) {
        return [...acc, option];
      }
      // check if any of the food values match the search input
      const filteredFoods = option.foods.filter((food) =>
        food.value.toLowerCase().includes(query.toLowerCase())
      );
      if (filteredFoods.length > 0) {
        return [...acc, { ...option, foods: filteredFoods }];
      }
      return acc;
    }, []);

    filteredOptions = [...tempFilteredOptions];
  };
</script>

<div class="container">
  <ul class="selected-options">
    <li>Beef and Mustard Pie</li>
    <li>Beef and Oyster Pie</li>
    <li>Ayam Percik</li>
    <li>Brown Stew Chicken</li>
    <li>Chicken & Mushroom Hotpot</li>
  </ul>
  <div class="list">
    <div class="list-input">
      <input
        on:focus={handleFocus}
        on:blur={handleBlur}
        on:input={(e) => handleChange(e)}
        value={query}
        type="text"
        placeholder="Search Your Favorite Books"
      />
    </div>
    <div class="list-options {isFocus ? ' show' : ' hidden'}">
      {#each filteredOptions as option (option.category)}
        <h3>{option.category}</h3>
        <ul>
          {#each option.foods as food (food.id)}
            <li>{food.value}</li>
          {/each}
        </ul>
      {/each}
    </div>
  </div>
</div>

<style>
  .container {
    display: flex;
    width: 720px;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }

  .selected-options {
    display: flex;
    gap: 12px;
    overflow-x: scroll;
    list-style: none;
    padding: 0;
    max-width: 83%;
  }

  .selected-options li {
    text-align: center;
    list-style: none;
    min-width: fit-content;
    padding: 4px 8px;
    color: #fff;
    border-radius: 10px;
    font-weight: 600;
    background-color: #14b8a6;
    margin-bottom: 5px;
  }

  .list {
    width: 100%;
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
  }

  .show {
    display: block;
  }

  .hidden {
    display: none;
  }

  ::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
    background-color: #f5f5f5;
  }

  ::-webkit-scrollbar {
    height: 5px;
    width: 5px;
    background-color: #0d9488;
  }

  ::-webkit-scrollbar-thumb {
    background-color: #0d9488;
    border: 2px solid #0d9488;
  }

  .list-input {
    width: 80%;
    margin-top: 20px;
    background-color: #ffffff;
    border-radius: 30px;
    padding: 5px 10px;
    display: flex;
    align-items: center;
  }

  .list-input input {
    width: 100%;
    margin: 0;
    border: none;
  }

  input:focus {
    outline: none;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .list-options {
    background-color: #fff;
    border-radius: 5px;
    margin-top: 6px;
    width: 83%;
    position: absolute;
    top: 60px;
    max-height: 300px;
    overflow-y: scroll;
  }

  .list-options h3 {
    margin: 0;
    border-bottom: #dbdbdb 1px solid;
    padding: 5px;
    background-color: #0d9488;
    color: white;
  }

  .list-options ul li {
    margin: 0;
    padding: 5px 20px;
    display: flex;
    align-items: center;
    border-bottom: #dbdbdb 1px solid;
    cursor: pointer;
  }

  .list-options ul li:hover {
    background-color: #14b8a6;
    color: white;
  }
</style>
