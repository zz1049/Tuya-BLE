# Fork changes (based on ShonP40/Tuya-BLE @ c095e8b)
1. Every half-set-up BLE client is now disconnected (time-boxed) when notify/device-info/pairing fails (upstream leaked it).
2. 3 attempts per cycle (was 100), 2 s apart; then exponential cooldown 10 s -> 600 s (circuit breaker). Resets on success.
3. One reconnect task and one resend task at a time (was a new task per error).
4. Missing Tuya GATT characteristics no longer fall through to start_notify; GATT cache is refreshed on the next attempt.
5. Repeated identical errors logged at most once per 60 s (rest at DEBUG).
6. Kept your own device mapping from the installed version: product id mknd4lci (Fingerbot Plus, switch = dp 1, others as the Plus) in devices.py, plus its Fingerbot switch entity (dp 1) in switch.py. Without this the fan would not press.
7. Kept your install's disabled options-update listener in __init__.py (line commented out).
