stage('Debug Environment') {
    steps {
        bat '''
            echo ===== PATH =====
            echo %PATH%
            echo ===== COMSPEC =====
            echo %ComSpec%
            echo ===== WHERE CMD =====
            where cmd
            echo ===== DIRECT CMD TEST =====
            C:\\Windows\\System32\\cmd.exe /c echo CMD WORKS
        '''
    }
}