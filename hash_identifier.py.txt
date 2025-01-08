import re

# Define hash regex patterns for detection
HASH_PATTERNS = {
    "MD5": r"^[a-fA-F\d]{32}$",
    "SHA-1": r"^[a-fA-F\d]{40}$",
    "SHA-256": r"^[a-fA-F\d]{64}$",
    "SHA-512": r"^[a-fA-F\d]{128}$",
    "bcrypt": r"^\$2[ayb]\$.{56}$",
    "NTLM": r"^[a-fA-F\d]{32}$",
}

def identify_hash(hash_string):
    """
    Identify the hash type based on regex patterns.
    :param hash_string: The hash string to analyze.
    :return: A list of possible hash types.
    """
    possible_hashes = []
    for hash_type, pattern in HASH_PATTERNS.items():
        if re.match(pattern, hash_string):
            possible_hashes.append(hash_type)
    return possible_hashes

def main():
    print("Welcome to Hash Identifier Tool!")
    print("Enter a hash to identify its type or type 'exit' to quit.")
    
    while True:
        hash_input = input("\nEnter the hash: ").strip()
        if hash_input.lower() == "exit":
            print("Exiting... Have a great day!")
            break
        possible_hashes = identify_hash(hash_input)
        
        if possible_hashes:
            print(f"The given hash matches the following types: {', '.join(possible_hashes)}")
        else:
            print("Hash type not identified. It may be unsupported or invalid.")

if __name__ == "__main__":
    main()
