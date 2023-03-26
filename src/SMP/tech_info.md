# The tech we would use

- The state of the entire system is verified via a hash chain
    - the hash chain will be formed via the `keccak256` of all of the state hashes of all of the devices in the system
- on-device software written in C++ or Rust for speed
- built for the ARM architecture
- our main platform will be built in JavaScript, C++, Python
    - Servers will be on-premises and backups on the cloud
- We will have an API for C/C++, C#, Java, Lisp, MATLAB, Pascal, Python, Rust, HDLs (Future Integration for Carbon)
    - API will also allow clients to deploy their own custom code to decide what information they want to be sent (via JSON or Binary) to their devices to control them based on updates/alerts on our platform
    - This can be done on our own in-app code platform or on separate, device-specific software
- We will use mapping to display the location of devices