#include QMK_KEYBOARD_H

#include "keymap.h"
#include "oneshot.h"
#include "swapper.h"

// clang-format off
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [DEF] = LAYOUT_split_3x6_3(
    // ╭────────┬────────┬────────┬────────┬────────┬────────╮                     ╭────────┬────────┬────────┬────────┬────────┬────────╮
        XXXXXXX ,NO_Q    ,NO_W    ,NO_E    ,NO_R    ,NO_T    ,                      NO_Y    ,NO_U    ,NO_I    ,NO_O    ,NO_P    ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,NO_A    ,NO_S    ,NO_D    ,NO_F    ,NO_G    ,                      NO_H    ,NO_J    ,NO_K    ,NO_L    ,NO_OSTR ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,NO_Z    ,NO_X    ,NO_C    ,NO_V    ,NO_B    ,                      NO_N    ,NO_M    ,NO_ARNG ,NO_AE   ,NO_DOT  ,XXXXXXX ,
    // ╰────────┴────────┴────────┴────────┼────────┼────────┼────────╮   ╭────────├────────┼────────┼────────┴────────┴────────┴────────╯
                                            XXXXXXX ,LA_NAV  ,KC_LSFT ,    KC_SPC  ,LA_NUM  ,XXXXXXX
    //                                     ╰────────┴────────┴────────╯   ╰────────┴────────┴────────╯
    ),
    [NAV] = LAYOUT_split_3x6_3(
    // ╭────────┬────────┬────────┬────────┬────────┬────────╮                     ╭────────┬────────┬────────┬────────┬────────┬────────╮
        XXXXXXX ,SW_APP  ,SW_WIN  ,SW_PTAB ,SW_NTAB ,XXXXXXX ,                      KC_ESC  ,KC_HOME ,KC_END  ,TR_JMPF ,TR_JMPB ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,OS_SHFT ,OS_CTRL ,OS_ALT  ,OS_CMD  ,TR_COPY ,                      KC_LEFT ,KC_DOWN ,KC_UP   ,KC_RGHT ,KC_BSPC ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,EMOJI   ,XXXXXXX ,XXXXXXX ,TR_TMUX ,TR_PAST ,                      KC_TAB  ,TR_SCDN ,TR_SCUP ,XXXXXXX ,KC_ENT  ,MO(CFG) ,
    // ╰────────┴────────┴────────┴────────┼────────┼────────┼────────╮   ╭────────├────────┼────────┼────────┴────────┴────────┴────────╯
                                            XXXXXXX ,KC_TRNS ,KC_LSFT ,    KC_SPC  ,LA_SYM  ,XXXXXXX
    //                                     ╰────────┴────────┴────────╯   ╰────────┴────────┴────────╯
    ),
    [NUM] = LAYOUT_split_3x6_3(
    // ╭────────┬────────┬────────┬────────┬────────┬────────╮                     ╭────────┬────────┬────────┬────────┬────────┬────────╮
        XXXXXXX ,XXXXXXX ,NO_7    ,NO_8    ,NO_9    ,XXXXXXX ,                      XXXXXXX ,NO_TILD ,NO_ACUT ,NO_GRV  ,NO_CIRC ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,XXXXXXX ,NO_4    ,NO_5    ,NO_6    ,XXXXXXX ,                      XXXXXXX ,OS_CMD  ,OS_ALT  ,OS_CTRL ,OS_SHFT ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,XXXXXXX ,NO_1    ,NO_2    ,NO_3    ,NO_0    ,                      XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,MO(CFG) ,
    // ╰────────┴────────┴────────┴────────┼────────┼────────┼────────╮   ╭────────├────────┼────────┼────────┴────────┴────────┴────────╯
                                            XXXXXXX ,LA_SYM  ,KC_LSFT ,    KC_SPC  ,KC_TRNS ,XXXXXXX
    //                                     ╰────────┴────────┴────────╯   ╰────────┴────────┴────────╯
    ),
    [SYM] = LAYOUT_split_3x6_3(
    // ╭────────┬────────┬────────┬────────┬────────┬────────╮                     ╭────────┬────────┬────────┬────────┬────────┬────────╮
        XXXXXXX ,NO_EXLM ,NO_DQOU ,NO_HASH ,NO_DLR  ,NO_PERC ,                      NO_AMPR ,NO_SLSH ,NO_LPAR ,NO_RPAR ,NO_EQL  ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,NO_QUES ,NO_QUOT ,NO_ASTR ,NO_SEMI ,NO_PLUS ,                      NO_DOT  ,NO_PIPE ,NO_LCBR ,NO_RCBR ,NO_AT   ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,NO_LABK ,NO_RABK ,NO_CLON ,NO_USCR ,NO_MINS ,                      NO_COMM ,NO_BLSH ,NO_LBRC ,NO_RBRC ,NO_DOT  ,MO(CFG) ,
    // ╰────────┴────────┴────────┴────────┼────────┼────────┼────────╮   ╭────────├────────┼────────┼────────┴────────┴────────┴────────╯
                                            XXXXXXX ,KC_TRNS ,KC_LSFT ,    KC_SPC  ,KC_TRNS ,XXXXXXX
    //                                     ╰────────┴────────┴────────╯   ╰────────┴────────┴────────╯
    ),
    [CFG] = LAYOUT_split_3x6_3(
    // ╭────────┬────────┬────────┬────────┬────────┬────────╮                     ╭────────┬────────┬────────┬────────┬────────┬────────╮
        XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,                      XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,QK_BOOT ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,                      XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,
    // ├────────┼────────┼────────┼────────┼────────┼────────┤                     ├────────┼────────┼────────┼────────┼────────┼────────┤
        XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,                      XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,XXXXXXX ,KC_TRNS ,
    // ╰────────┴────────┴────────┴────────┼────────┼────────┼────────╮   ╭────────├────────┼────────┼────────┴────────┴────────┴────────╯
                                            XXXXXXX ,KC_TRNS ,XXXXXXX ,    XXXXXXX ,KC_TRNS ,XXXXXXX
    //                                     ╰────────┴────────┴────────╯   ╰────────┴────────┴────────╯
    ),
};
// clang-format on

bool is_oneshot_cancel_key(uint16_t keycode) {
  switch (keycode) {
  case KC_ESC:
    return true;
  default:
    return false;
  }
}

bool is_oneshot_ignored_key(uint16_t keycode) {
  switch (keycode) {
  case LA_NUM:
  case LA_NAV:
  case LA_SYM:
  case KC_LSFT:
  case OS_SHFT:
  case OS_CTRL:
  case OS_ALT:
  case OS_CMD:
    return true;
  default:
    return false;
  }
}

bool sw_app_active = false;
bool sw_win_active = false;

oneshot_state os_shft_state = os_up_unqueued;
oneshot_state os_ctrl_state = os_up_unqueued;
oneshot_state os_alt_state = os_up_unqueued;
oneshot_state os_cmd_state = os_up_unqueued;

bool process_record_user(uint16_t keycode, keyrecord_t *record) {
  update_swapper(&sw_app_active, KC_LGUI, KC_TAB, SW_APP, keycode, record);
  update_swapper(&sw_win_active, KC_LGUI, NO_QUOT, SW_WIN, keycode, record);

  update_oneshot(&os_shft_state, KC_LSFT, OS_SHFT, keycode, record);
  update_oneshot(&os_ctrl_state, KC_LCTL, OS_CTRL, keycode, record);
  update_oneshot(&os_alt_state, KC_LALT, OS_ALT, keycode, record);
  update_oneshot(&os_cmd_state, KC_LCMD, OS_CMD, keycode, record);

  return true;
}
