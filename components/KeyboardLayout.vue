<script setup>
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const props = defineProps({
  // One entry per click step: { id, needShift, hlChar }
  // id       — matches a key id in the rows data below
  // needShift — whether Shift is required (makes Shift keys glow)
  // hlChar   — character to show large on the key when highlighted
  keys: {
    type: Array,
    default: () => [],
  },
})

const { $clicks } = useSlideContext()

const UNIT = 44   // px per 1u key width
const H    = 40   // key height px
const GAP  =  3   // gap between keys px

function kw(u) {
  return `${u * UNIT - GAP}px`
}

// id        — unique key identifier
// bot       — label shown on the lower part of the key
// top       — shift-layer label shown small in top-left (null for letters/fn)
// w         — width in units
// hlChar    — character to show large when this key is highlighted
// needShift — whether Shift is required to produce hlChar
const rows = [
  [
    { id: 'esc',    bot: 'Esc',  top: null, w: 1.5  },
    { id: 'f1',     bot: 'F1',   top: null, w: 1    },
    { id: 'f2',     bot: 'F2',   top: null, w: 1    },
    { id: 'f3',     bot: 'F3',   top: null, w: 1    },
    { id: 'f4',     bot: 'F4',   top: null, w: 1    },
    { id: 'f5',     bot: 'F5',   top: null, w: 1    },
    { id: 'f6',     bot: 'F6',   top: null, w: 1    },
    { id: 'f7',     bot: 'F7',   top: null, w: 1    },
    { id: 'f8',     bot: 'F8',   top: null, w: 1    },
    { id: 'f9',     bot: 'F9',   top: null, w: 1    },
    { id: 'f10',    bot: 'F10',  top: null, w: 1    },
    { id: 'f11',    bot: 'F11',  top: null, w: 1    },
    { id: 'f12',    bot: 'F12',  top: null, w: 1    },
    { id: 'del',    bot: 'Del',  top: null, w: 1.5  },
  ],
  [
    { id: 'grave',  bot: '`',    top: '~',  w: 1    },
    { id: 'n1',     bot: '1',    top: '!',  w: 1    },
    { id: 'n2',     bot: '2',    top: '@',  w: 1    },
    { id: 'n3',     bot: '3',    top: '#',  w: 1    },
    { id: 'n4',     bot: '4',    top: '$',  w: 1    },
    { id: 'n5',     bot: '5',    top: '%',  w: 1    },
    { id: 'n6',     bot: '6',    top: '^',  w: 1    },
    { id: 'n7',     bot: '7',    top: '&',  w: 1    },
    { id: 'n8',     bot: '8',    top: '*',  w: 1    },
    { id: 'n9',     bot: '9',    top: '(',  w: 1    },
    { id: 'n0',     bot: '0',    top: ')',  w: 1    },
    { id: 'minus',  bot: '-',    top: '_',  w: 1    },
    { id: 'equals', bot: '=',    top: '+',  w: 1    },
    { id: 'bksp',   bot: '⌫',   top: null, w: 2    },
  ],
  [
    { id: 'tab',    bot: 'Tab',  top: null, w: 1.5  },
    { id: 'q',      bot: 'Q',    top: null, w: 1    },
    { id: 'w',      bot: 'W',    top: null, w: 1    },
    { id: 'e',      bot: 'E',    top: null, w: 1    },
    { id: 'r',      bot: 'R',    top: null, w: 1    },
    { id: 't',      bot: 'T',    top: null, w: 1    },
    { id: 'y',      bot: 'Y',    top: null, w: 1    },
    { id: 'u',      bot: 'U',    top: null, w: 1    },
    { id: 'i',      bot: 'I',    top: null, w: 1    },
    { id: 'o',      bot: 'O',    top: null, w: 1    },
    { id: 'p',      bot: 'P',    top: null, w: 1    },
    { id: 'lbr',    bot: '[',    top: '{',  w: 1    },
    { id: 'rbr',    bot: ']',    top: '}',  w: 1    },
    { id: 'bslash', bot: '\\',   top: '|',  w: 1.5  },
  ],
  [
    { id: 'caps',   bot: 'Caps', top: null, w: 1.75 },
    { id: 'a',      bot: 'A',    top: null, w: 1    },
    { id: 's',      bot: 'S',    top: null, w: 1    },
    { id: 'd',      bot: 'D',    top: null, w: 1    },
    { id: 'f',      bot: 'F',    top: null, w: 1    },
    { id: 'g',      bot: 'G',    top: null, w: 1    },
    { id: 'h',      bot: 'H',    top: null, w: 1    },
    { id: 'j',      bot: 'J',    top: null, w: 1    },
    { id: 'k',      bot: 'K',    top: null, w: 1    },
    { id: 'l',      bot: 'L',    top: null, w: 1    },
    { id: 'semi',   bot: ';',    top: ':',  w: 1    },
    { id: 'quote',  bot: "'",    top: '"',  w: 1    },
    { id: 'enter',  bot: 'Enter',top: null, w: 2.25 },
  ],
  [
    { id: 'lshift', bot: 'Shift',top: null, w: 2.25 },
    { id: 'z',      bot: 'Z',    top: null, w: 1    },
    { id: 'x',      bot: 'X',    top: null, w: 1    },
    { id: 'c',      bot: 'C',    top: null, w: 1    },
    { id: 'v',      bot: 'V',    top: null, w: 1    },
    { id: 'b',      bot: 'B',    top: null, w: 1    },
    { id: 'n',      bot: 'N',    top: null, w: 1    },
    { id: 'm',      bot: 'M',    top: null, w: 1    },
    { id: 'comma',  bot: ',',    top: '<',  w: 1,   hlChar: '<', needShift: true  },
    { id: 'period', bot: '.',    top: '>',  w: 1,   hlChar: '>', needShift: true  },
    { id: 'slash',  bot: '/',    top: '?',  w: 1,   hlChar: '/', needShift: false },
    { id: 'rshift', bot: 'Shift',top: null, w: 2.75 },
  ],
  [
    { id: 'lctrl',  bot: 'Ctrl', top: null, w: 1.25 },
    { id: 'lwin',   bot: '⊞',   top: null, w: 1.25 },
    { id: 'lalt',   bot: 'Alt',  top: null, w: 1.25 },
    { id: 'space',  bot: '',     top: null, w: 6.25 },
    { id: 'ralt',   bot: 'Alt',  top: null, w: 1.25 },
    { id: 'rwin',   bot: '⊞',   top: null, w: 1.25 },
    { id: 'menu',   bot: '☰',   top: null, w: 1.25 },
    { id: 'rctrl',  bot: 'Ctrl', top: null, w: 1.25 },
  ],
]

// Fast lookup: key id → prop entry (for hlChar, needShift)
const keyMap = computed(() =>
  Object.fromEntries(props.keys.map(k => [k.id, k]))
)

// All keys introduced so far (clicks accumulate)
const highlighted = computed(() => {
  const s = new Set()
  props.keys.forEach((k, i) => {
    if ($clicks.value >= i + 1) s.add(k.id)
  })
  return s
})

// Shift keys glow when the step being introduced requires Shift
const shiftGlow = computed(() => {
  const step = props.keys[$clicks.value - 1]
  return step?.needShift === true
})

function keyStyle(key) {
  const isHL    = highlighted.value.has(key.id)
  const isShift = (key.id === 'lshift' || key.id === 'rshift') && shiftGlow.value

  return {
    width:           kw(key.w),
    height:          H + 'px',
    borderRadius:    '4px',
    display:         'flex',
    flexDirection:   'column',
    alignItems:      'center',
    justifyContent:  'flex-end',
    paddingBottom:   '5px',
    position:        'relative',
    userSelect:      'none',
    transition:      'background-color 0.35s, color 0.35s, box-shadow 0.35s, transform 0.25s',
    backgroundColor: isHL    ? '#facc15'
                   : isShift ? '#4b3f14'
                   :           '#374151',
    color:           isHL    ? '#111827'
                   : isShift ? '#fde68a'
                   :           '#d1d5db',
    boxShadow:       isHL
                       ? '0 0 0 2px #fde047, 0 4px 8px rgba(0,0,0,0.4)'
                       : isShift
                         ? '0 0 0 1px #854d0e'
                         : '0 2px 3px rgba(0,0,0,0.4)',
    transform:       isHL ? 'translateY(-3px) scale(1.08)' : 'none',
    zIndex:          isHL ? 1 : 0,
  }
}

function topStyle(key) {
  const isHL = highlighted.value.has(key.id)
  return {
    position:   'absolute',
    top:        '3px',
    left:       '4px',
    fontSize:   '14px',
    lineHeight: '1',
    color:      isHL ? '#92400e' : '#9ca3af',
    fontWeight: isHL ? 'bold' : 'normal',
  }
}

function botStyle(key) {
  const isHL = highlighted.value.has(key.id)
  return {
    fontSize:   isHL ? '18px' : '10px',
    lineHeight: '1',
    fontWeight: isHL ? '900' : 'normal',
    transition: 'font-size 0.25s',
  }
}
</script>

<template>
  <div style="display: inline-block; font-family: monospace;">
    <div
      v-for="(row, ri) in rows"
      :key="ri"
      :style="{ display: 'flex', gap: GAP + 'px', marginBottom: ri < rows.length - 1 ? GAP + 'px' : '0' }"
    >
      <div
        v-for="key in row"
        :key="key.id"
        :style="keyStyle(key)"
      >
        <span v-if="key.top" :style="topStyle(key)">{{ key.top }}</span>
        <span :style="botStyle(key)">
          {{ highlighted.has(key.id) && (keyMap[key.id]?.hlChar ?? key.hlChar) ? (keyMap[key.id]?.hlChar ?? key.hlChar) : key.bot }}
        </span>
      </div>
    </div>
  </div>
</template>
