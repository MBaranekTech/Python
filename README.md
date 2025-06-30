# 🔍 Python Palindrome String

1)
On Job Interview you can be asked for a palindrome string -> is a string that reads the same forwards and backwards <br>
(racecar -> racecar). <br>
Interviewers use this to test if you understand: <br>
String manipulation (s[::-1], loops) <br>
Data structures (lists, stacks, queues) <br>
Python built-in functions <br>


```
def isPalindrome(s):
  return s == s[::-1]

print(isPalindrome ("racecar"))
```
# 🔍 Monitor Registry for Active Camera Use with Python Script
2)
Windows tracks webcam access in the registry at: <br>
no admin required <br>

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\webcam\NonPackaged
```
Each app gets a subkey. If the LastUsedTimeStop value is 0, it means the app is currently using the camera. <br>

📦 Python Script to Detect Active Webcam Use
```
import winreg
import time

def is_camera_in_use():
    try:
        base_key_path = r"Software\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\webcam\NonPackaged"
        with winreg.OpenKey(winreg.HKEY_CURRENT_USER, base_key_path) as base_key:
            i = 0
            while True:
                try:
                    subkey_name = winreg.EnumKey(base_key, i)
                    with winreg.OpenKey(base_key, subkey_name) as subkey:
                        value, _ = winreg.QueryValueEx(subkey, "LastUsedTimeStop")
                        if value == 0:
                            return True
                    i += 1
                except OSError:
                    break
    except Exception as e:
        print(f"Error reading registry: {e}")
    return False

# 🟢 Main loop to monitor every 2 seconds
if __name__ == "__main__":
    print("Monitoring camera usage (Ctrl+C to stop)...")
    while True:
        if is_camera_in_use():
            print("📷 Camera is currently in use!")
        else:
            print("✅ Camera is not in use.")
            time.sleep(2)
```
