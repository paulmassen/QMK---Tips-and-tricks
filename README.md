# QMK - Tips-and-tricks
A collection of notes, tips and hacks for customizing a keyboard running the QMK firmware.

## General Notes

```
LEADER_EXTERNS();
// Declare a boolean variable to keep track of whether any sequence
// will have been matched.
bool did_leader_succeed;
void matrix_scan_user(void) {
  LEADER_DICTIONARY() {
    // Initialize did_leader_succeed as well as leading to be false
    did_leader_succeed = leading = false;
    // Replace the sequences below with your own sequences.
    SEQ_ONE_KEY(KC_T) {
      SEND_STRING(SS_LCTRL(SS_LSFT("t")));
      // In each sequence, set our flag to true. This way, we'll
      // know when any sequence was matched.
      did_leader_succeed = true;
    }
    SEQ_TWO_KEYS(KC_N, KC_T) {
      SEND_STRING(SS_LCTRL("t"));
      did_leader_succeed = true;
    }
    // Call leader_end at the end of the function, instead of at
    // the start. This way, we're sure we have set did_leader_succeed.
    leader_end();
  }
}
void leader_end(void) {
  if (did_leader_succeed) {
    // If any sequence was matched, did_leader_succeed will have
    // been set to true up in the matrix_scan_user function.
    // Put your code for a matched leader key sequence here.
  } else {
    // If no sequence was matched, did_leader_succeed will not
    // have been set to true anywhere, so we'll end up here.
    // Put your code for an unmatched leader key sequence here.
  }
}
```

# Using it in French

# Credits & References

https://thomasbaart.nl/2018/12/13/qmk-basics-tap-dance/
