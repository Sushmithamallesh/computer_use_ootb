- Add proper browser initialization to ease automation
- Add mulitple tab management support


## TODO: Fix Async/Sync Mismatch in Tool Execution
### Issue
- Task context mismatch error in asyncio cleanup
- Error occurs after successful tool execution
- Not blocking functionality but needs cleanup

### Files to Modify
1. `computer_use_demo/tools/collection.py`
   - Make `run()` sync instead of async
   
2. `computer_use_demo/tools/computer.py`
   - Make `screenshot()` consistently sync
   - Update other async methods if needed

3. `computer_use_demo/autopc/executor/anthropic_executor.py`
   - Remove async loop management
   - Update to use sync tool execution

### Approach
Choose one consistent approach:
- Option 1: Make everything sync (recommended)
  - Change ToolCollection.run() to be sync
  - Keep screenshot() sync
  - Remove async/await from chain

- Option 2: Make everything async
  - Keep ToolCollection.run() async
  - Make screenshot() async
  - Make executor's __call__ async

Priority: Low (Not blocking functionality)