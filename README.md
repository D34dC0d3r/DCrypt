# DCrypt
DCrypt (D34d Crypter) is an advanced .NET executable file crypter written in Rust. I created it for educational purposes as part of an academic cybersecurity project, but I decided to edit and support it further after the school project ended. The aim of the project is to apply the latest techniques to avoid detection.


The crypter implements a number of advanced mechanisms designed to hinder static and dynamic analysis and to evade detection by antivirus software:

- Strong Encryption: The payload (a .NET exe) is encrypted using the AES-256-GCM algorithm.

- Key Derivation: The encryption key is generated dynamically using Argon2id with a random salt for each encryption, ensuring that two identical input files will produce completely different encrypted outputs.

- Code Polymorphism: Before each compilation, key functions in the stub (the loader) are given random names. This significantly complicates signature-based detection.

- In-Memory Execution: The encrypted payload is decrypted and executed directly in the process memory. At no point is the decrypted .exe written to disk, which bypasses file-scanning antivirus. (Currently experiencing difficulties)

Anti-analysis Techniques:

- Anti-Debug: The stub checks whether it is running under a debugger (IsDebuggerPresent). If so, it exits immediately.

-Anti-Sandbox: The program deliberately delays execution by 30–60 seconds. Many automated analysis sandboxes terminate a program after a short time, so the analysis ends before the actual payload runs.


I encrypted the payload I created in [DcRat](https://github.com/qwqdanchun/DcRat). I am sending the Kleenscan AV scan [HERE](https://kleenscan.com/scan_result/56663128b3b3e8ade7bd5609d46914bd9bec5e952b505eca702516e26093b531)

<img width="923" height="571" alt="image" src="https://github.com/user-attachments/assets/f164c2d1-0a8d-4c39-b880-7c783493d7de" />

If anyone knows how to do memory injection in Windows 11, please let me know. I will gladly reward you with free file encryption :D
I tried patching Windows 11, MEM_IMG, and MEM_PRIV... but it still doesn't work for me.

Comparison with an unencrypted file in DnSpy.


<img width="514" height="675" alt="image" src="https://github.com/user-attachments/assets/315cf067-b9b1-4a29-ba27-b44172ff7eae" />
