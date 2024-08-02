
https://teams.microsoft.com/l/meetup-join/19%3ameeting_ZTdmYWQyMTEtM2NlZi00MDY4LWJkNGItZTU4NGJmZjZhYWQ3%40thread.v2/0?context=%7b%22Tid%22%3a%22658ba197-6c73-4fea-91bd-1c7d8de6bf2c%22%2c%22Oid%22%3a%222b8c6555-bd49-48ad-af87-688cdb03681d%22%7d

def calculateScore(text, prefixString, suffixString):
    def longest_suffix_prefix_match(text, prefixString, suffixString):
        # Find longest match for prefix score
        max_prefix_score = 0
        prefix_match = ""
        for i in range(len(prefixString)):
            if text.startswith(prefixString[i:]):
                score = len(prefixString) - i
                if score > max_prefix_score:
                    max_prefix_score = score
                    prefix_match = prefixString[i:]

        # Find longest match for suffix score
        max_suffix_score = 0
        suffix_match = ""
        for i in range(1, len(suffixString) + 1):
            if text.endswith(suffixString[:i]):
                score = i
                if score > max_suffix_score:
                    max_suffix_score = score
                    suffix_match = suffixString[:i]

        return prefix_match, suffix_match, max_prefix_score, max_suffix_score

    max_score = 0
    result = text

    for i in range(len(text)):
        for j in range(i + 1, len(text) + 1):
            substring = text[i:j]
            prefix_match, suffix_match, prefix_score, suffix_score = longest_suffix_prefix_match(substring, prefixString, suffixString)
            current_score = prefix_score + suffix_score
            if current_score > max_score or (current_score == max_score and substring < result):
                max_score = current_score
                result = substring

    return result

# Sample Input
text = "nothing"
prefixString = "bruno"
suffixString = "ingenious"

# Expected Output: "nothing"
print(calculateScore(text, prefixString, suffixString))

# Sample Input
text = "ab"
prefixString = "b"
suffixString = "a"

# Expected Output: "a"
print(calculateScore(text, prefixString, suffixString))
