<script>
export default {
  name: 'MotyHeading',
  functional: true,
  props: {
    headingText: {
      type: String,
      default: ''
    },
    headingPosition: {
      type: String,
      default: 'center'
    },
    baseSize: {
      type: String,
      default: 'medium'
    },
    level: {
      type: String,
      default: '2'
    }
  },
  render(h, context) {
    const { headingText, headingPosition, baseSize, level } = context.props
    const mergeClasses = classes => {
      let contextClasses = context.data.staticClass ? ' ' + context.data.staticClass : ''
      contextClasses += context.data.class ? ' ' + context.data.class : ''
      return contextClasses ? `${classes} ${contextClasses}` : classes
    }
    const position =
      headingPosition === 'center'
        ? 'text-center'
        : headingPosition === 'left'
        ? 'text-left'
        : 'text-right'

    const size =
      baseSize === 'medium'
        ? 'moty-display-medium-bold'
        : baseSize === 'small'
        ? 'moty-display-small-bold'
        : 'moty-display-large-bold'

    const headingClass = mergeClasses(`mb-3 text-moty-darker ${position} ${size}`)
    return h(
      'h' + level,
      {
        'v-balance-text': true,
        class: headingClass
      },
      [headingText]
    )
  }
}
</script>
