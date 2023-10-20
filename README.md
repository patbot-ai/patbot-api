Server: https://patbot.org

### 1. Get an authentication cookie for a new anonymous account. The same cookie must be sent in all subsequent requests

    GET /

Response body: undefined (should be discarded)

### 2. Get list of available modules

    GET /api/get_module_list

Response body: JSON
    
    {"module_list": [module_id_1, module_id_2, ...],
     "module_name_list": [module_name_1, module_name_2, ...]}

- `module_id` is internally used to keep track of the current module
- `module_name` is the text for how to display the module

### 3. Initialize chat and get chat history
    GET /api/initialize_chat

Response body: JSON

    {'message_history': [{"role": ..., "content": ..., "uuid": ...}, ...],
     'feedback_history': ...,
     'module': ...,
     'button_options': [...]}

### 4. Submit a chat message

    GET /api/process_user_message?msg=...

Response body: JSON

    {"module": ...,
     "text_responses": [{"role": ..., "content": ..., "uuid": ...}],
     "button_options": [...],
     "disable_typing": ...}`

- `role` is either "user" or "assistant" (PATbot)
- `button_options` are suggested responses
- `disable_typing` is a boolean whether or not `button_options` are required responses, if `true` then users must select one of the suggested responses

### 5. Switch module

    GET /api/process_switch_module?module=...&module_name=...

- `module` and `module_name` are the same ones from /api/get_module_list

Response body: Same as /api/process_user_message

