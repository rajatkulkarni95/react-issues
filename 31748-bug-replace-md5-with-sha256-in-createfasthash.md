# Bug: Replace md5 with sha256 in createFastHash().

> Issue #31748 - Created on 12/13/2024

> Original URL: https://github.com/facebook/react/issues/31748

## Description

1.MD5 has potential collision risks.
2.Even for speed considerations, MD5 is slower than SHA256, so replacing MD5 with SHA256 is worthwhile.
code at:https://github.com/facebook/react/blob/e06c72fcf4632ad3117add713a25f6354631f037/packages/react-server/src/ReactServerStreamConfigNode.js#L234-L238
Below are the speed test results(:
#### String Length: 16
MD5 Average Time: 0.0148 ms
SHA256 Average Time: 0.0131 ms

#### String Length: 256
MD5 Average Time: 0.0193 ms
SHA256 Average Time: 0.0175 ms

#### String Length: 10000
MD5 Average Time: 0.5830 ms
SHA256 Average Time: 0.4030 ms

#### String Length: 100000
MD5 Average Time: 6.2866 ms
SHA256 Average Time: 4.6130 ms

code is
```
<!DOCTYPE html>
<html>
<head>
    <title>Hash Function Test</title>
    <!-- Include the CryptoJS library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
</head>
<body>
    <h1>Hash Function Performance Test</h1>
    <div id="results"></div>

    <script>
        const md5 = (str) => CryptoJS.MD5(str).toString();
        const sha256 = (str) => CryptoJS.SHA256(str).toString();

        // Generate a random string of specified length
        function getRandomString(length) {
            let result = '';
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            for (let i = 0; i < length; i++) {
                result += characters.charAt(Math.floor(Math.random() * characters.length));
            }
            return result;
        }

        // Test the performance of the hash function
        function testHashFunction(func, length, iterations = 1000) {
            let total = 0;
            const data = getRandomString(length); // Generate data once outside the loop
            const startTime = performance.now();

            for (let i = 0; i < iterations; i++) {
                func(data); // Reuse the same data for all iterations
            }

            const endTime = performance.now();
            total = endTime - startTime; // Calculate total time once
            const average = total / iterations;
            return average;
        }

        // Test different string lengths
        const lengths = [16, 256, 10000, 100000];
        const resultsElement = document.getElementById('results');

        lengths.forEach(length => {
            const md5Avg = testHashFunction(md5, length);
            const sha256Avg = testHashFunction(sha256, length);

            resultsElement.innerHTML += `
                <h2>String Length: ${length}</h2>
                <p>MD5 Average Time: ${md5Avg.toFixed(4)} ms</p>
                <p>SHA256 Average Time: ${sha256Avg.toFixed(4)} ms</p>
                <hr>
            `;
        });
    </script>
</body>
</html>
```

