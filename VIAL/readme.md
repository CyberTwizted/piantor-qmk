Added tap dance to outer keys, see the updated keymap below. \Added KC_TRNS to outer columns for subsequent layers so they have access to ctrl and shift. 
\Ideally, in a QMK flash, the tap dance would be custom so that the hold is instant, and the tap + hold tapping term can be set manually. \I was able to implement this in VIAL by setting the tap dance to On Tap : LShift, On tap + hold : LCtrl
The Numbers and Symbols layers could probably be combined since we now have access to shift on all layers.
  - This could also open up the possibilty to put a tap dance on the unused layer, in this case tap would be delete and tap and hold would be ctrl.


Custom qmk tapdance example:

## PsudoCode
```
[Press]
↓
Start timer

If key held for >10ms → Shift

If tapped (released quickly)
→ Start second timer

If re-pressed within 200ms → Ctrl
```

Custom tap dance handler in QMK format:

```
enum {
    TD_SHIFT_CTRL = 0,
};

qk_tap_dance_action_t tap_dance_actions[] = {
    [TD_SHIFT_CTRL] = ACTION_TAP_DANCE_FN_ADVANCED(NULL, td_shift_ctrl_finished, td_shift_ctrl_reset)
};

static uint16_t td_timer;
static bool ctrl_ready = false;
static bool shift_active = false;

void td_shift_ctrl_finished(qk_tap_dance_state_t *state, void *user_data) {
    if (state->count == 1) {
        if (state->interrupted || !state->pressed) {
            // Quick tap - start waiting for re-hold
            ctrl_ready = true;
            td_timer = timer_read();
        } else {
            // Held - treat as shift
            register_code(KC_LSFT);
            shift_active = true;
        }
    }
}

void td_shift_ctrl_reset(qk_tap_dance_state_t *state, void *user_data) {
    if (ctrl_ready && timer_elapsed(td_timer) < 200) {
        register_code(KC_LCTL);
        unregister_code(KC_LCTL);
    }

    if (shift_active) {
        unregister_code(KC_LSFT);
        shift_active = false;
    }

    ctrl_ready = false;
}

```


## Keyboard layout
#include QMK_KEYBOARD_H

#define HM_A LGUI_T(KC_A)
#define HM_R LALT_T(KC_R)
#define HM_S LCTL_T(KC_S)
#define HM_T LSFT_T(KC_T)
#define HM_N RSFT_T(KC_N)
#define HM_E RCTL_T(KC_E)
#define HM_I RALT_T(KC_I)
#define HM_O RGUI_T(KC_O)

#define MediaL_ESC LT(1, KC_ESC)
#define NavL_SPC LT(2, KC_SPC)
#define MouseL_TAB LT(3, KC_TAB)
#define SymL_ENT LT(4, KC_ENT)
#define NumL_BSPC LT(5, KC_BSPC)
#define FuncL_DEL LT(6, KC_DEL)

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {

// Layer 0: Base - Colemak-DH
[0] = LAYOUT_split_3x6_3(
  KC_LALT,     KC_Q,   KC_W,   KC_F,   KC_P,   KC_B,       KC_J,   KC_L,   KC_U,     KC_Y,   KC_SCLN,  KC_RALT,
  KC_TD(8),    HM_A,   HM_R,   HM_S,   HM_T,   KC_G,       KC_M,   HM_N,   HM_E,     HM_I,   HM_O,     TD(9),
  KC_LGUI,     KC_Z,   KC_X,   KC_C,   KC_D,   KC_V,       KC_K,   KC_H,   KC_COMM,  KC_DOT, KC_SLSH,  TG(7),
                MediaL_ESC, NavL_SPC, MouseL_TAB,             SymL_ENT, NumL_BSPC, FuncL_DEL
),

// Layer 1: Media
[1] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_R, KC_M,    KC_H,    KC_S,    KC_V,    KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_E, KC_MRWD, KC_VOLD, KC_VOLU, KC_MFFD, KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_O, KC_0,    KC_1,    KC_2,    KC_3,    KC_TRNS,
                     KC_NO, KC_NO, KC_NO,             KC_MSTP, KC_MPLY, KC_MUTE
),

// Layer 2: Navigation
[2] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      C(KC_Y), C(KC_V), C(KC_C), C(KC_X), C(KC_Z), KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_CAPS, KC_LEFT, KC_DOWN, KC_UP,   KC_RGHT, KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_INS,  KC_HOME, KC_PGDN, KC_PGUP, KC_END,  KC_TRNS,
                     KC_NO, KC_NO, KC_NO,             KC_ENT, KC_BSPC, KC_DEL
),

// Layer 3: Mouse
[3] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      C(KC_Y), C(KC_V), C(KC_C), C(KC_X), C(KC_Z), KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_NO, KC_MS_L, KC_MS_D, KC_MS_U, KC_MS_R, KC_TRNS,
  KC_TRNS, KC_NO, KC_NO, KC_NO, KC_NO, KC_NO,      KC_NO, KC_WH_L, KC_WH_D, KC_WH_U, KC_WH_R, KC_TRNS,
                     KC_NO, KC_NO, KC_NO,             KC_BTN2, KC_BTN1, KC_BTN3
),

// Layer 4: Symbols
[4] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_LCBR, KC_AMPR, KC_ASTR, KC_LPRN, KC_RCBR,    KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_COLN, KC_DLR,  KC_PERC, KC_CIRC, KC_PLUS,    KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_TILD, KC_EXLM, KC_AT,   KC_HASH, KC_PIPE,    KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
                         KC_LPRN, KC_RPRN, KC_UNDS,           KC_NO, KC_NO, KC_NO
),

// Layer 5: Numbers
[5] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_LBRC, KC_7, KC_8, KC_9, KC_RBRC,    KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_SCLN, KC_4, KC_5, KC_6, KC_EQL,     KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_GRV,  KC_1, KC_2, KC_3, KC_BSLS,    KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
                    KC_DOT, KC_0, KC_MINS,           KC_NO, KC_NO, KC_NO
),

// Layer 6: Function
[6] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_F12, KC_F7, KC_F8, KC_F9, KC_PSCR,     KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_F11, KC_F4, KC_F5, KC_F6, KC_SLCK,     KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
  KC_TRNS, KC_F10, KC_F1, KC_F2, KC_F3, KC_PAUS,     KC_NO, KC_NO, KC_NO, KC_NO, KC_NO, KC_TRNS,
                     KC_APP, KC_SPC, KC_TAB,            KC_NO, KC_NO, KC_NO
)


// Added as a separate vial file
// Layer 7: Qwerty
[7] = LAYOUT_split_3x6_3(
  KC_TRNS, KC_Q,  KC_W,  KC_E,  KC_R,  KC_T,      KC_Y,  KC_U,  KC_I,    KC_O,    KC_P,    KC_TRNS,
  KC_TRNS, KC_A,  KC_S,  KC_D,  KC_F,  KC_G,      KC_H,  KC_J,  KC_K,    KC_L,    KC_SCLN, KC_TRNS,
  KC_TRNS, KC_Z,  KC_X,  KC_C,  KC_V,  KC_B,      KC_N,  KC_M,  KC_COMM, KC_DOT,  KC_SLSH, KC_TRNS
               KC_TRNS, KC_TRNS, KC_TRNS,            KC_TRNS, KC_TRNS, KC_TRNS
)

};
