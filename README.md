# Bloxd-Yapper
HOW TO MAKE A RNG CODE
// Get the name of the entity (player) who triggered this script
let name = api.getEntityName(myId);

// Generate a random number between 1 and 100 to determine what card the player will get
let roll = Math.floor(Math.random() * 100) + 1;

// Define the possible card types, each with a block type, custom display name, description, and color
let blocks = [
    { block: "Red Carpet",   "custom Display Name": "Warrior Card",          "custom Description": "Balanced melee fighter. (Common)", color: "red" },
    { block: "Blue Carpet",  "custom Display Name": "Archer Card",           "custom Description": "Long-range expert. (Common)", color: "blue" },
    { block: "Yellow Carpet","custom Display Name": "Scout Card",            "custom Description": "Fast and agile. (Common)", color: "yellow" },
    { block: "Green Carpet", "custom Display Name": "Assassin Card",         "custom Description": "High damage, low health. (Uncommon)", color: "green" },
    { block: "Lime Carpet",  "custom Display Name": "Tank Card",             "custom Description": "High defense, slow movement. (Uncommon)", color: "lime" },
    { block: "Purple Carpet","custom Display Name": "Healer Card",           "custom Description": "Supports allies with healing. (Rare)", color: "purple" },
    { block: "Pink Carpet",  "custom Display Name": "Mage Card",             "custom Description": "Master of magic attacks. (Rare)", color: "pink" },
    { block: "Black Carpet", "custom Display Name": "Necromancer Card",      "custom Description": "Controls the dead. (Epic)", color: "black" },
    { block: "White Carpet", "custom Display Name": "Paladin Card",          "custom Description": "Holy warrior with defense. (Epic)", color: "white" },
    { block: "Gray Carpet",  "custom Display Name": "Rising Dead Card",      "custom Description": "Going back to life, stealing others' life. You are the Immortal.", color: "gray" },
];

// Define the probability ranges for each card
let chances = [
    { min: 1,  max: 9 },    // Warrior (9%)
    { min: 10, max: 18 },   // Archer (9%)
    { min: 19, max: 26 },   // Scout (8%)
    { min: 27, max: 38 },   // Assassin (12%)
    { min: 39, max: 53 },   // Tank (15%)
    { min: 54, max: 63 },   // Healer (10%)
    { min: 64, max: 72 },   // Mage (9%)
    { min: 73, max: 81 },   // Necromancer (9%)
    { min: 82, max: 90 },   // Paladin (9%)
    { min: 91, max: 100 },  // Rising Dead (10%)
];

// Loop through the chances array to find which range the roll falls into
for (let i = 0; i < chances.length; i++) {
    let range = chances[i];

    // If the roll is within this range, assign the corresponding card
    if (roll >= range.min && roll <= range.max) {
        let reward = blocks[i];  // Get the matching card block
        let displayName = reward["custom Display Name"];  // Get custom name
        let description = reward["custom Description"];    // Get description
        let color = reward.color;                          // Get display color

        // Notify the player with a colored message about their reward
        api.sendMessage(myId, `You Caught A ${displayName}! ${description}`, { color: color });

        // Give the player the corresponding item with metadata
        api.giveItem(myId, reward.block, 1, {
            customDisplayName: displayName,
            customDescription: description,
        });

        break;  // Stop the loop since we've found the matching reward
    }
}
