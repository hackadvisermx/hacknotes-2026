Crypto secure starts with "semantic security". That's an SAT-level word, but it's really just winning a guessing game.

The semantic security game is running at [here](http://rsac-challenges.picoctf.net:49914/).




## Solve
```python
import requests
import json

BASE_URL = "http://rsac-challenges.picoctf.net:49914/"  # Replace with actual URL

class CPAAttacker:
    def __init__(self):
        self.session = requests.Session()
        self.score = 0
        
    def encrypt(self, m0, m1):
        """Get encryption of either m0 or m1"""
        resp = self.session.post(f"{BASE_URL}/encrypt", 
                                json={"m0": m0, "m1": m1})
        return resp.json()["ciphertext"]
    
    def solve(self, guess):
        """Submit guess (0 or 1)"""
        resp = self.session.post(f"{BASE_URL}/solve", 
                                json={"guess": guess})
        result = resp.json()
        self.score = result.get("score", self.score)
        return result
    
    def get_status(self):
        """Get current score"""
        resp = self.session.get(f"{BASE_URL}/status")
        return resp.json()

def statistical_attack():
    attacker = CPAAttacker()
    
    # Choose two distinct but equal-length messages
    m0 = "AAAAA"
    m1 = "BBBBB"
    
    # Collect ciphertext statistics
    m0_samples = [attacker.encrypt(m0, m0) for _ in range(5)]
    m1_samples = [attacker.encrypt(m1, m1) for _ in range(5)]
    
    print("m0 samples:", m0_samples)
    print("m1 samples:", m1_samples)
    
    # Look for patterns (e.g., first few Base64 chars)
    m0_prefixes = [ct[:4] for ct in m0_samples]  # First 4 Base64 chars
    m1_prefixes = [ct[:4] for ct in m1_samples]
    
    print("m0 prefixes:", m0_prefixes)
    print("m1 prefixes:", m1_prefixes)
    
    # Now play rounds
    while attacker.score < 10:
        # Get challenge
        challenge_ct = attacker.encrypt(m0, m1)
        challenge_prefix = challenge_ct[:4]
        
        # Guess based on which distribution it matches
        m0_match = m0_prefixes.count(challenge_prefix)
        m1_match = m1_prefixes.count(challenge_prefix)
        
        guess = 0 if m0_match > m1_match else 1
        
        result = attacker.solve(guess)
        print(f"Score: {attacker.score}, Guess: {guess}")
        
        if "flag" in result:
            print(f"FLAG: {result['flag']}")
            break

# Run the attack
statistical_attack()
```