# Deck

```java

public enum Suit {
	Club (0), Diamond (1), Heart (2), Spade (3);
	private int value;
	private Suit(int v) {
		this.value = v;
	}

	public int getValue() {
		return this.value;
	}

	public static Suit getSuitFromValue(int value) {};
}

public class Deck <T extends Card> {
	private ArrayList<T> cards;
	private int dealltIndex = 0;

	public void setDeckOfCards(ArrayList<T> deckOfCards) {}

	public void shuffle() {}
	public int remainingCards() {
		return cards.size() - dealtIndex;
	}

	public T[] dealHand(int number) {}
	public T dealCard() {}
}

public abstract class Card {
	private boolean available = true;

	protected int faceValue;
	protected Suit suit;

	public Card(int c, Suit s) {
		faceValue = c;
		suit = s;
	}
}


```