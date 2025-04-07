# malaysian-slang-dictionary
import json

class SlangDictionary:
    def __init__(self, file_name="malaysian_slang.json"):
        self.file_name = file_name
        self.load_data()

    def load_data(self):
        try:
            with open(self.file_name, "r", encoding="utf-8") as file:
                self.slang_words = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.slang_words = {}

    def save_data(self):
        with open(self.file_name, "w", encoding="utf-8") as file:
            json.dump(self.slang_words, file, indent=4, ensure_ascii=False)

    def add_slang(self, word, meaning):
        self.slang_words[word] = meaning
        self.save_data()
        print(f"Added: {word} - {meaning}")

    def get_meaning(self, word):
        return self.slang_words.get(word, "Word not found in dictionary.")

    def list_slang(self):
        if not self.slang_words:
            print("No slang words recorded.")
            return
        for word, meaning in self.slang_words.items():
            print(f"{word}: {meaning}")

# Example usage
def main():
    dictionary = SlangDictionary()
    while True:
        print("\nMalaysian Slang Dictionary")
        print("1. Add Slang Word")
        print("2. Get Meaning")
        print("3. List All Slang Words")
        print("4. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            word = input("Enter slang word: ")
            meaning = input("Enter meaning: ")
            dictionary.add_slang(word.strip(), meaning.strip())
        elif choice == "2":
            word = input("Enter slang word: ")
            print(dictionary.get_meaning(word.strip()))
        elif choice == "3":
            dictionary.list_slang()
        elif choice == "4":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
345
