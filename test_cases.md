# FraudShield AI – Test Cases

These are illustrative test cases for checking the prototype. Actual results may vary depending on the detection rules and whether the Gemini API is configured.

| ID | Sample input | Expected checks | Expected risk |
|---|---|---|---|
| TC-01 | "Congratulations! You won cashback. Click this shortened link and enter your UPI PIN." | Reward claim, shortened link, request for UPI PIN | High |
| TC-02 | "Your KYC will expire today. Update immediately using this link." | Urgency, KYC pressure, link | Medium/High |
| TC-03 | "Share your OTP to receive your payment." | OTP request | High |
| TC-04 | "Your electricity bill is due. Please pay through your official provider app." | No obvious scam indicators in this sample | Low |
| TC-05 | "Payment of Rs. 250 received successfully." | No obvious scam indicators in this sample | Low |
| TC-06 | "You have won a free gift. Pay a small processing fee to claim it." | Prize claim, payment pressure | Medium/High |

## How to run these tests

1. Start the Flask application using the instructions in `README.md`.
2. Paste each sample message into the message-analysis box.
3. Click the analyze button.
4. Check the risk band, score, warning signs, and safety advice.
5. Record the actual result and compare it with the expected checks above.

## Important notes

- These are synthetic examples, not real user messages.
- A low-risk result does not prove that a message is safe.
- A high-risk result is a warning, not a definitive fraud finding.
- Never test with real OTPs, UPI PINs, passwords, bank details, or private messages.
- Do not use the prototype as a substitute for verification through an official bank or payment-provider channel.
