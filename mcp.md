Overview: MCP and Remote Command Execution
What We're Trying to Do:
We're setting up Home Assistant to act as a bridge that allows executing shell commands on a remote Linux computer using the MCP (Multimodal Conversation Protocol) interface. Specifically:
A client (mcp_test.py) sends an MCP command to Home Assistant
Home Assistant receives this as a HassRunCommand intent with parameters
Home Assistant forwards the command to a LNXlink client on a remote Linux computer via MQTT
LNXlink executes the command and returns the result back via MQTT
Home Assistant captures this result and returns it to the MCP client
What We've Done So Far:
Added Custom Intent Script: Created a HassRunCommand intent in Home Assistant's configuration.yaml
Configured Slot Definitions: Defined slots for "value" (the command) and "timeout"
Added Conversation Integration: Added configuration to expose our custom intent to the conversation/MCP component
Made Multiple Syntax Adjustments: Tried different ways to access slot values
Simplified for Testing: Currently using a simplified version that just echoes back what command would be executed
Current Status:
✅ The HassRunCommand tool appears in available tools list when running mcp_test.py
✅ Other tools like HassTurnOn/HassTurnOff work correctly (can control lights)
❌ The HassRunCommand tool returns an error when called with parameters
➡️ We've simplified the integration to test basic slot handling before reintroducing MQTT
Current Configuration (Simplified for Testing):
Apply to configuratio...
Next Steps for Implementation:
Verify Simplified Version: Test if the basic slot handling works with the simplified implementation
Confirm MQTT Integration: Ensure MQTT is properly configured in Home Assistant
Verify LNXlink Setup: Confirm LNXlink client is running and listening on expected MQTT topics
Incrementally Add Back Functionality: Once basic tests pass, gradually reintroduce MQTT publishing, waiting for response, etc.
Test End-to-End Flow: Finally test the complete path from MCP → Home Assistant → LNXlink → command execution → response
Once we have the simplified version working, we'll know if the issue is with basic intent handling or with the MQTT/LNXlink communication.




intent_script:
  HassRunCommand:
    description: "Runs a shell command on a specified LNXlink client"
    slots:
      value:
        description: "The shell command to execute"
        required: true
      timeout:
        description: "Timeout in seconds"
        required: false
    action:
      - variables:
          test_response: "This is a test response. Command would have been: {{ value }}"
    speech:
      text: "{{ test_response }}"

conversation:
  intents:
    expose:
      - HassRunCommand