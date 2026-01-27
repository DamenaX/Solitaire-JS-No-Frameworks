# Solitaire JS No Framewroks

This is a small, self-contained Javascript project built with the intentional constraint of not using frameworks or ANY external libraries, my focus was primarily on **understanding the essence of javascript and first-principles implementation without relying on the abstractions given by the popular frameworks.**

## The Game
The project is an implementation of the cards game known as Solitaire, specifically the Klondike Solitarie (NOT Spider Solitaire). 

Klondike is the most well-known solitaire variant, played with a single deck of cards where the goal is to move all cards to four foundation piles organized by suit from Ace to King. Cards are dealt into seven tableau columns with increasing numbers of face-down cards, and players build descending sequences in alternating colors while uncovering hidden cards. Additional cards are drawn from a stock pile, and careful planning is required to manage limited moves and gradually expose and organize the deck.

For detailed rules and history, see the
[Klondike (solitaire) Wikipedia article](https://en.wikipedia.org/wiki/Klondike_(solitaire)).


<img width="1538" height="691" alt="image" src="https://github.com/user-attachments/assets/cdece356-b1fe-493b-a84b-167a72b9eadb" />
<img width="1894" height="843" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/cb5c5158-63b1-4e1e-a39e-02e54d849a51" />
<img width="1889" height="842" alt="Screenshot (46)" src="https://github.com/user-attachments/assets/48b8b885-6c72-449e-a459-02dbec4a14e5" />

## Tech Stack

- Logic and DOM: Vanilla Javascript  
- Styling: CSS (no libraries/frameworks)

## Scope & Limitations

- More verbose than framework-based solutions  
- Minimal tooling by design  
- Optimized for understanding, obviously not for scale

## Technical Implementation

* **State Management via Plain Data Structures**
  Game state is tracked using simple arrays:

  * `deckArr` for the stock pile
  * `activePlaceArr` for the seven tableau columns
  * `foundationPlaceArr` for the four foundation piles
    No external state managers or abstractions are used.

* **Card Identity Encoding**
  Cards are represented as string IDs (e.g. `AH`, `10S`, `QC`), with rank and suit parsed dynamically using helper functions.

* **Custom Deck Initialization & Shuffle Algorithm**
  A full 52-card deck is generated programmatically and shuffled using a manual unique-index randomization process rather than built-in helpers.

* **DOM-Driven Rendering Model**
  Cards are rendered as `<img>` elements and positioned via inline styles to simulate stacking. Face-down cards are handled through CSS classes and image swapping.

* **Native Drag & Drop API**
  Card movement relies on the browser’s native Drag and Drop API:

  * Captures the dragged card ID
  * Dynamically determines and moves stacked cards below it
  * Resolves drop targets at runtime

* **Rule Enforcement at Move Time**
  Move validation is performed imperatively during the drop event:

  * Rank progression is checked numerically
  * Suit matching is enforced for foundation piles
  * Empty tableau placement is restricted appropriately

* **Progressive Card Reveal Logic**
  After successful moves, previously hidden cards are automatically flipped by updating their DOM state and image source.

* **Stock / Waste Cycling**
  Stock cards are revealed one at a time, with waste pile recycling handled explicitly through array and DOM manipulation.

* **Win Condition Detection**
  The game continuously checks foundation pile lengths to detect completion and trigger a win state overlay.

* **Game Reset & Reinitialization**
  A full reset reconstructs all state arrays, clears DOM containers, rebinds event listeners, and reinitializes the deck.

* **Intentional Absence of Abstractions**
  All logic, rendering, and interaction handling are implemented directly to expose the underlying mechanics of JavaScript, the DOM, and browser events.



