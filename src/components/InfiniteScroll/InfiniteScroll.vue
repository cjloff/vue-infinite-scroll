<template>
    <section>
        <slot></slot>
        <div ref="trigger" style="height: 1px"></div>
    </section>
</template>

<script>
    export default {
        props: {
            currentIndex: {
                type: Number,
                required: true
            },
            lastIndex: {
                type: Number,
                required: true
            }
        },
        data:function() {
            return {
                observer: null
            }
        },
        mounted() {
            this.observer = new IntersectionObserver(entries => {
                if (entries[0].isIntersecting) {
                    this.$emit('update')
                }
            })
            this.observer.observe(this.$refs.trigger);
        },
        watch: {
            currentIndex(value) {
                if(value === this.lastIndex) {
                    this.observer.unobserve(this.$refs.trigger);
                }
            }
        }
    }
</script>


