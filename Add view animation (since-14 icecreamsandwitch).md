##  object/view animation  (IceCreamSandwitch api 14)

Simple code isn't it ?

        mButton.animate()
                .alpha(0f)
                .translationY(-mButton.getHeight())
                .setDuration(getResources().getInteger(
                        android.R.integer.config_shortAnimTime))
                .withEndAction(new Runnable() {
                    @Override
                    public void run() {

                    }
                });