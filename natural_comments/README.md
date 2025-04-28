# Natural Comments Skill

This skill for Wingman aims to make interactions feel more natural by having the AI proactively comment or ask questions during periods of silence, similar to a human co-pilot or friend. It can optionally use screenshots to inform its comments about the user's current activity.

## Features

*   **Proactive Comments:** Automatically generates comments or questions when the user has been silent for a random duration (between configurable minimum and maximum thresholds).
*   **Conversation Focus:** Prioritizes continuing the existing conversation topic based on recent history.
*   **Vision Capability (Optional):** Can take screenshots of the user's primary monitor to make comments more relevant to the current visual context (e.g., games, videos, coding). Uses a refined prompting strategy to avoid commenting on static screens unless necessary.
*   **Configurable Behavior:** Allows customization of silence thresholds, maximum number of proactive comments between user interactions, and vision settings.
*   **Manual Control:** Provides voice commands to turn the commenting behavior on or off.
*   **Status Check:** Allows querying the current status (active/inactive) and silence timers.
*   **Forced Comment:** Allows manually triggering a comment attempt.
*   **Custom System Prompt:** Allows overriding the default system prompt for advanced customization.

## Functionality

### ⚠️ Cost Warning ⚠️

**If you provide your own API key for the underlying Wingman (e.g., OpenAI), enabling the `Enable Vision` setting may incur costs.** When vision is enabled, the skill periodically captures screenshots and sends them to the AI model for analysis during periods of silence (before the `Max Proactive Messages` limit is reached). This image analysis can be significantly more expensive than text-only interactions. Disable the `Enable Vision` setting if you want to avoid these potential vision-related costs.

## Configuration (`default_config.yaml`)

The following settings can be adjusted in the skill's configuration:

*   `min_silence_threshold_seconds` (integer, default: 60): Minimum seconds of silence before a proactive comment might be triggered.
*   `max_silence_threshold_seconds` (integer, default: 180): Maximum seconds of silence before a proactive comment might be triggered. The actual trigger time is randomized between min and max.
*   `max_proactive_messages` (integer, default: 3): Maximum number of proactive comments the skill will make before requiring user interaction to reset the count.
*   `vision_enabled` (boolean, default: True): Whether to enable screenshot capture and analysis for comments.
*   `vision_display_to_capture` (integer, default: 1): Which monitor display to capture (1 = primary, 2 = secondary, etc.).
*   `add_comments_to_history` (boolean, default: True): Whether the proactive comments made by this skill should be added to the main conversation history.
*   `auto_start` (boolean, default: True): Whether the skill should start monitoring for silence automatically when Wingman loads.
*   `custom_system_prompt` (string, optional, default: None): Allows providing a completely custom system prompt to guide the LLM's comment generation. If left blank, a refined default prompt focusing on natural conversation is used.

## Voice Commands (Tools)

*   **"Turn on comments"**: Enables the proactive commenting feature.
*   **"Turn off comments"**: Disables the proactive commenting feature.
*   **"What is the natural comment status?"**: Reports whether the skill is active, the time since the last message, the target silence duration, and the current proactive comment count.
*   **"Force natural comment"**: Manually triggers an attempt to generate a proactive comment immediately (bypasses silence timer and count limit for this one instance).

## Dependencies

This skill requires the following Python libraries:

*   `mss`: For taking screenshots efficiently.
*   `Pillow`: For image processing (resizing screenshots).

These should be installed in your Wingman environment. If using `pip`, you can typically install them with:
`pip install mss Pillow`

## Usage

1.  Enable the skill in Wingman.
2.  Adjust settings in `default_config.yaml` as needed (requires Wingman restart after changes).
3.  If `auto_start` is true (default), the skill will begin monitoring silence automatically.
4.  Use the voice commands to control the skill during runtime. 