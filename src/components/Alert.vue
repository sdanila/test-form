<template>
  <div class="notification" :class="className">
    <div class="notification__content">
      <div class="content__text">
        <span>{{msg}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Alert',
  props: {
    className: String,
    msg: String,
  }
}
</script>

<style lang="sass">
.notification
  position: fixed
  width: 15%
  height: 10%
  border-radius: 5px
  bottom: 7%
  left: 4%
  text-align: center
  display: flex
  justify-content: center
  align-items: center
  span
    color: white
.error
  background-color: #dc0f0f
.success
  background-color: green
@media (max-width: 991px)
  .notification
    width: 22%
    height: 7%
    // left: 3vh
@media (max-width: 574px)
  .notification
    width: 42%
    left: 28%
  span
    font-size: 12px
</style>