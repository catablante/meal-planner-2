# meal-planner-2
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

const meals = [
  { day: "Monday", meal: "Spaghetti with Garlic Bread", cost: "$6", ingredients: ["Pasta", "Tomato Sauce", "Garlic Bread"] },
  { day: "Tuesday", meal: "Chicken & Rice Bowl", cost: "$7", ingredients: ["Chicken Breast", "Rice", "Vegetables"] },
  { day: "Wednesday", meal: "Taco Night", cost: "$5", ingredients: ["Tortillas", "Ground Beef", "Cheese", "Lettuce"] },
  { day: "Thursday", meal: "Vegetable Stir Fry", cost: "$6", ingredients: ["Mixed Vegetables", "Soy Sauce", "Rice"] },
  { day: "Friday", meal: "Homemade Pizza", cost: "$8", ingredients: ["Pizza Dough", "Tomato Sauce", "Cheese", "Toppings"] },
  { day: "Saturday", meal: "Grilled Cheese & Tomato Soup", cost: "$4", ingredients: ["Bread", "Cheese", "Tomato Soup"] },
  { day: "Sunday", meal: "Baked Potatoes & Chili", cost: "$7", ingredients: ["Potatoes", "Canned Chili", "Cheese"] }
];

const randomMeals = [
  "Mac & Cheese with Broccoli",
  "Egg Fried Rice",
  "Lentil Soup & Bread",
  "Sloppy Joes",
  "Pasta Salad",
  "Quesadillas",
  "Baked Ziti"
];

export default function MealPlanner() {
  const [mealPlan, setMealPlan] = useState(meals);
  const [shoppingList, setShoppingList] = useState([]);

  const swapMeal = (index) => {
    const newMeal = prompt("Enter a new meal suggestion:");
    if (newMeal) {
      const updatedPlan = [...mealPlan];
      updatedPlan[index] = { ...updatedPlan[index], meal: newMeal, ingredients: [] };
      setMealPlan(updatedPlan);
    }
  };

  const generateShoppingList = () => {
    const ingredients = mealPlan.flatMap((meal) => meal.ingredients);
    setShoppingList([...new Set(ingredients)]);
  };

  const suggestRandomMeal = () => {
    const randomMeal = randomMeals[Math.floor(Math.random() * randomMeals.length)];
    alert(`Try this meal: ${randomMeal}`);
  };

  return (
    <div className="p-6 max-w-2xl mx-auto">
      <h1 className="text-xl font-bold mb-4">Budget-Friendly Meal Planner</h1>
      <div className="grid gap-4">
        {mealPlan.map((item, index) => (
          <Card key={index} className="p-4 shadow-md">
            <CardContent className="flex justify-between items-center">
              <div>
                <h2 className="text-lg font-semibold">{item.day}</h2>
                <p>{item.meal} - <span className="font-bold">{item.cost}</span></p>
              </div>
              <Button onClick={() => swapMeal(index)}>Swap</Button>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="mt-6 flex gap-4">
        <Button onClick={generateShoppingList}>Generate Shopping List</Button>
        <Button onClick={suggestRandomMeal}>Suggest a Meal</Button>
      </div>
      {shoppingList.length > 0 && (
        <div className="mt-6 p-4 bg-gray-100 rounded">
          <h2 className="text-lg font-bold">Shopping List</h2>
          <ul className="list-disc pl-5">
            {shoppingList.map((item, index) => (
              <li key={index}>{item}</li>
            ))}
          </ul>
        </div>
      )}
    </div>
  );
}
